Coding for the First Tech Challenge is usually an ongoing process. Revisions are made all the time to mirror the advancements in the robot over the course of the season. Because of this, it is highly important to remain organized when programming, to make sure that your code is readable for yourself, and more importantly for others. 

I cannot stress the importance of commenting your code. Even though it can be tedious, short comments explaining what parts of the code do go a long way. They help the original programmer quickly recall what the program does, and helps anyone else who is looking at the code understand what it does. 

In my opinion, the best way to organize code is by using OOP (Object Oriented Programming), or at least some concepts from the overall premise. The main thing to take away from this organization style is to separate the various subsystems of the robot into their own classes. 

This is an example of how I organize the subsystems in my team's codebase:

subsystems  
 ┣ Aligner.java  
 ┣ Drive.java  
 ┣ Intake.java  
 ┣ Lift.java  
 ┣ Odometry.java  
 ┣ PID.java  
 ┗ Robot.java  

Each of the subsystems is a class that behaves independently from the other subsystems. The different classes are all instantiated in Robot.java, which serves as the overarching class.

This way of organizing the code means that any singular subsystem can be instantiated when necessary, while maintaining its state across the codebase. Changes only need to be made in the above classes, and will affect any place where they are called. 