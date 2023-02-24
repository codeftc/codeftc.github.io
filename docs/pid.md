PID control is one of the most common control systems you will see in robotics, and FTC specifically. Three values need to be tuned (Proportional, Integral and Derivative) which alter the behavior of the controller. 

Earlier, we saw an example of a proportional controller, which can be seen modelled below:

![proportional controller diagram](https://www.tutorialspoint.com/control_systems/images/proportional_controller.jpg)

The Kp value is the only one altering the controller's input. Alternatively, a PID controller uses 2 more values, Ki and Kd. The PID controller can be modelled as seen below:

![PID controller](https://miro.medium.com/max/1400/1*K_yaMyOkUNJzBpjutSmpwQ.png)

To gain a comprehensive understanding of the math behind PID controllers, I recommend you watch <a href="https://www.youtube.com/watch?v=UR0hOmjaHp0" target="_blank">this</a> Youtube video series, which explains the fundamental mathematical concept very well.

Lets go ahead and program a simple PID controller in Java:

```java
public class PID {
    private double Kp;
    private double Ki;
    private double Kd;
    private double integralSum = 0.0;
    private double lastError = 0.0;
    
    private ElapsedTime timer;

    public PID(double p, double i, double d) {
        Kp = p;
        Ki = i;
        Kd = d;
        timer = new ElapsedTime();
        timer.reset();
    }

    public double getValue(double error) {
        double dT = timer.seconds();
        double derivative = (error - lastError) / dT;

        // sum all the error over time
        integralSum += (error * dT);

        // return the out value eg. motor power
        double out = (Kp * error) + (Ki * integralSum) + (Kd * derivative);

        lastError = error;
        timer.reset();

        return out;
    }
}
```

Although you can code your own PID controller like done above, I recommend you instead use the PID controller from FTCLib, a library for First Tech Challenge robotics. Follow the Kookybotz tutorial <a href="https://www.youtube.com/watch?v=E6H6Nqe6qJo&t=347s" target="_blank">video</a> to see how you can setup FTCLib in your project. 

A rule of thumb when programming is to never reinvent the wheel. There are tons of incredible libraries and tools out there for your use, created by the amazing FTC community. Why try to make something from scratch when you can use a pre-existing tool that will save you a lot of time?