Roadrunner is a great option for coding autonomous paths, especially if you are new to control theory concepts. However, coding paths from scratch can be much more rewarding, and gives you full control and understanding of your code. 

Linked is my team's control function (MoveTo), which allows us to specify a target x, y, and heading.
<a href="https://github.com/millburnx/CenterStage/blob/master/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/ctrl/MoveTo.java" target="_blank">[code]</a>

Using a trapezoidal motion profile, simple linear movement can be achieved. For more complex movement such as splines, path information can be combined with motion profiles to create trajectories. The robot can then follow these trajectories, which output information about what the robot should be doing at a current moment in time (position, velocity, and acceleration).