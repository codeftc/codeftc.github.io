The base of any FTC robot is the drivetrain, which is what enables the robot to move around. Drivetrains can be split into two types: differential and holonomic.
![tank vs. mecanum](https://2589213514-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-MHCAE012xNfg1h3SM9v%2F-MHHjkw3y4bMwQm17duZ%2F-MHITU8RoRkSW0c5Hy-6%2FDrivetrain%20Compare.svg?alt=media&token=ba03c7e2-d288-447a-afcd-fe40b2135286)

##Differential

Differential, or tank, drivetrains typically use traction wheels, and do not possess the ability to strafe. They are usually easier to program, but limit mobility. An example can be seen below:

![tank drivetrain](https://2589213514-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-MHCAE012xNfg1h3SM9v%2F-MiTCk2u-IxN8HHM6Pr1%2F-MicMUh1962c97yDjtRJ%2FStarter%20Kit%20Robot%20V5%20-%20drivetrain.svg?alt=media&token=10cd2b80-4ef4-4e3e-8867-602cfd3aa0c6)

As you can see, the tank drivetrain would not possess the ability to strafe due to the traction and omniwheels used. The above pictured drive would have the ability to move forwards and backwards, and turn.

Lets go ahead and program movement for a tank drivetrain:

```java
@TeleOp
public class DifferentialDrive extends LinearOpMode {
    @Override
    public void runOpMode() throws InterruptedException {
        // declare four motors for each of our wheels
        DcMotor frontLeft = hardwareMap.dcMotor.get("frontLeft");
        DcMotor frontRight = hardwareMap.dcMotor.get("frontRight");
        DcMotor backLeft = hardwareMap.dcMotor.get("backLeft");
        DcMotor backRight = hardwareMap.dcMotor.get("backRight");

        // reverse the right motors
        frontRight.setDirection(DcMotorSimple.Direction.REVERSE);
        backRight.setDirection(DcMotorSimple.Direction.REVERSE)

        waitForStart();

        if(isStopRequested()) return;

        while(opModeIsActive()) {
            frontLeft.setPower(gamepad.left_stick_y);
            backLeft.setPower(gamepad.left_stick_y);
            frontRight.setPower(gamepad.right_stick_y);
            backRight.setPower(gamepad.right_stick_y);
        }
    }
}
```

##Holonomic

Most FTC teams use holonomic drives which allow for strafing.

![mecanum drivetrain](https://cdn11.bigcommerce.com/s-eem7ijc77k/images/stencil/850w/products/2268/28241/3209-0001-0004-Schematic__96237.1613160104.png?c=2%201x,%20https://cdn11.bigcommerce.com/s-eem7ijc77k/images/stencil/1200w/products/2268/28241/3209-0001-0004-Schematic__96237.1613160104.png?c=2%202x)

The mecanum drive, as pictured above, is commonly used in FTC. This type of drive uses special mecanum wheels whose rollers are tilted at a 45° angle. When the wheels move in a specific arrangement, the drive strafes. 

![mecanum movement](https://gm0.org/en/latest/_images/mecanum-drive-directions.png)

Now let's write code for our mecanum drivetrain:

```java
@TeleOp
public class MecanumDrive extends LinearOpMode {
    @Override
    public void runOpMode() throws InterruptedException {
        // declare four motors for each of our wheels
        DcMotor frontLeft = hardwareMap.dcMotor.get("frontLeft");
        DcMotor frontRight = hardwareMap.dcMotor.get("frontRight");
        DcMotor backLeft = hardwareMap.dcMotor.get("backLeft");
        DcMotor backRight = hardwareMap.dcMotor.get("backRight");

        // reverse the right motors
        frontRight.setDirection(DcMotorSimple.Direction.REVERSE);
        backRight.setDirection(DcMotorSimple.Direction.REVERSE)

        waitForStart();

        if(isStopRequested()) return;

        while(opModeIsActive()) {
            frontLeft.setPower(gamepad.left_stick_y);
            backLeft.setPower(gamepad.left_stick_y);
            frontRight.setPower(gamepad.right_stick_y);
            backRight.setPower(gamepad.right_stick_y);
            move(gamepad.left_stick_y, gamepad.left_stick_x, gamepad.right_stick_x);
        }

        public void move(double power, double strafe, double turn) {
            double denominator = Math.max(Math.abs(power) + Math.abs(strafe) + Math.abs(turn), 1);
            double frontLeftPower = (power + strafe + turn) / denominator;
            double backLeftPower = (power - strafe + turn) / denominator;
            double frontRightPower = (power - strafe - turn) / denominator;
            double backRightPower = (power + strafe - turn) / denominator;

            setDrivePowers(frontLeftPower, backLeftPower, frontRightPower, backRightPower);
        }

        public void setDrivePowers(double frontLeftPower, double backLeftPower, double frontRightPower, double backRightPower) {
            leftFront.setPower(frontLeftPower);
            leftRear.setPower(backLeftPower);
            rightFront.setPower(frontRightPower);
            rightRear.setPower(backRightPower);
        }
    }
}
```

The mecanum drivetrain allows for much more freedom of movement, and makes quick manuevers during the teleop period possible.

