One of the most important concepts to understand when coding for any form of robotics or engineering is control theory. This concept allows you to have full control over a system, and a full understanding of this concept gives you the knowledge necessary to tackle a wide range of systems. For example, a motor can respond well to environmental feedback and change its power input accordingly. 

## Open-loop control

You have likely seen this form of control before. A motor is told to input a specific power for a specified duration of time. The motor will run for this period of time, and then stop. This example is illustrated below:

```java
// simple open-loop example

motor.setPower(1);
time(100)
motor.setPower(0);
```
In the above example, a motor is told to run for a specified duration, in this case 100 of some arbitrary unit. Although this type of control may have its uses, it is often not sufficient. This is because outside factors may influence the behaviour of the system, and cause it to stray the programmer's intended result.

## Closed-loop control

In order to combat this problem, a closed loop system can be created. In this type of system, the input is directly influenced by the output. For example, a motor will be given an input power of 1 until the angle of the motor is 90 degrees. The motor will correct itself based on feedback.

A proportional controller is a simple example of closed-loop control. The current position is referenced to the desired position, and error is calculated. The error is used as the input into the system, and slowly reaches 0.

```java
// simple proportional controller example

target = 10;

while(targetNotReached) {
    motorPosition = motor.getPosition();
    error = target - motorPosition;
    motor.setPower(error);
}
```

On the next page, I'll be going more in depth into closed-loop control.