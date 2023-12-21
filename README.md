# Lejos implementation with the EV3 and Java  
  
This is the project for the Applied project application course 4cr.  
Our team's objective was to bring the EV3 to life by working with Lejos. Our robot had to perform a series of tasks such as effectively detecting a line on the ground and following this path without deviating from it
and avoiding any obstacles on it's way.  
The programming aspect of this project was done using the Eclipse IDE and Java on the EV3 robot given to the groups.  
<br/>  

## Our Project Features    

#### _SlayRoboto_ 

Main program where all the threads are initialized: DataExchange(DE), LineFollower (LFObj), ObstacleDetector (ODObj), ColorSensor (CSObj)  


#### _DataExchange_ 
Collection of setters and getters. Here values are passed through the different threads.  
The robot is able to keep track of its cycles around the track through the count variable in this object. This is collected from the LineFollower thread.  

 
#### _ColorSensor_ 

Thread where the EV3ColorSensor is connected to the Sensor Port (S3). 
In the run method, we collect the data from the colour sensor and save the samples into an array. Doing so the robot is always checking the colour of line it is following and thus staying on track.  

#### _LineFollower_
Thread where we initialize the motors that will move the wheels of the robot (EV3LargeRegulatedMotor).  
There are 3 main points of the run method inside of this thread.  

**The first** one is making sure the robot will move smoothly on the line as long as there are no obstacles on the way. 

**Second point** is if the robot does detect obstacles, it stops following the line and begins to take action to avoid the obstacle with the objective of going back to the line afterwards.  

**Third point** is the celebration, it will happen when the robot gets the information from the DataExchange thread that it has seen the obstacle twice then it will start playing a little tune and spinning around to celebrate the end of its cycle.  

 

#### _ObstacleDetector_
Thread where the EV3UltrasonicSensor is connected to the Sensor Port (S1).  
With constant data collection through the sample provider, values are sent to the DataExchange thread to notify the robot if an obstacle has been detected and also if the distance of that obstacle falls below the security Distance.  
