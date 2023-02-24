Even armed with knowledge about control theory, programming autons can be tough. Roadrunner is a libary that simplifies the process, and gives you the ability to create efficient and accurate autons. The library also offers an easy way to tune drive constants such as track width, and PID for various controllers that it uses. 

The documentation for Roadrunner can be found <a href="https://learnroadrunner.com/" target="_blank">here</a>.

It is very important that Roadrunner is tuned properly for it to work well. I recommend that you spend time thoroughly following the tuning steps in the documentation I linked above. Once everything is tuned, creating paths is not very difficult. 

I have a few tips from my own experience using Roadrunner in the past.

Firstly, Roadrunner provides a sample mecanum drive class that can be used without much need for change. However, I recommend that you use the same drive class that you use in TeleOp. This means that changes you make in one drive class do not have to be replicated in the other. In order to use you own drive class, simply copy over the Roadrunner methods from the Sample Mecanum Drive class into your own drive class. 

Second, after you have gained a good understanding of how trajectories, and trajectory sequences work, make sure to use asynchronous trajectories whenever possible. This allows for the movement of other parts of the robot such as a lift or arm to happen simultaneously to the movement of the drive.