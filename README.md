# Final Project

Project Name : `Hand Gesture Navigation for turtlebot`

Team Members:
- Sarah Gifford, sg262@buffalo.edu
- Shivam Dave, sdave@buffalo.edu

---
## Project Objective
- Created a gesture navigation system that is based upon simple hand gestures that are read through the webcam on the computer running the code.
- You will also be able to control by saying "forward", "fullspeed", "halfspeed" and "stop".
- This code accurately turns hand movement into turtlebot movement. 

## Project Description

Link to Video Presentation - https://youtu.be/3iP7pm4viOU

This project allows one to navigate a turtlebot using simple hand gestures to navigate around a world. The project is implemented using  simple openCV library functions. As we have learnt in redball and followbot, we make the turtlebot follow a line or a ball using camera on the bot by defining the features to specifically look for in the images received in the bot. This code allow user to receive images from a webcam and apply some transformations to achieve required input to navigate the turtlebot.

### Contributions
- From the concepts and functions of OpenCV, this project captures simple hand gestures by detecting convexity defects on the contours recognized by the code.
- After assigning the type of movement to each gesture, for example 1 is assigned to move forward, 2 is assigned to rotate the turtlebot and similar movements for other gestures.
- Then a simple logic turns that detected gesture into turtlebot `twist()` command which is then published to move the turtlebot

![](gesturebot/Gesture.PNG)

--- 


## Installation Instructions

For voice control.
- Install Following Dependencies:

```
sudo apt-get install -y python python-dev python-pip build-essential swig libpulse-dev git
sudo pip install pyaudio
sudo pip install pocketsphinx
```



1. Create the Package:
    ```
    cd ~/catkin_ws/src
    catkin_create_pkg gesturebot rospy roscpp geometry_msgs sensor_msgs
    ```
    *Note that we have added some dependency packages, which will show up in `CMakeLists.txt` and `package.xml`.*
    
2. Let's go ahead and create our `scripts` directory:
    ```
    cd ~/catkin_ws/src/gesturebot
    mkdir scripts
    ```
        
3. Get the source code from the course github site (you will need to log on):
    ```
    cd ~/Downloads
    git clone https://github.com/IE-482-582/course-project-gifford_and_dave.git 
    
    ```
    
 4. Copy `package.xml` and the Python scripts to our workspace
    ```
    cd ~/Downloads/course-project-gifford_and_dave/gesturebot/
    cp package.xml ~/catkin_ws/src/gesturebot/
    cp scripts/* ~/catkin_ws/src/gesturebot/scripts/
    ```
    
 5. Make our Python scripts executable
    ```
    cd ~/catkin_ws/src/gesturebot/scripts
    chmod +x *.py
    ls
    ```
    
6. Compile/make our package 

    ```
    cd ~/catkin_ws
    catkin_make
 
--- 
## Running the Code
We will require 3 terminals for running this project.

- To enable camera and microphone in virtual machine 
	
    ```	
	VMWARE MENUBAR --> DEVICE --> WEBCAM --> SELECT WEBCAM (based on pc)
	VMWARE MENUBAR --> DEVICE --> AUDIO --> SELECT AUDIO INPUT (based on pc)
    ```	

- Terminal 1

  ```
  cd catkin_ws/src/gesturebot/scripts/
  roslaunch gesturebot maze.launch
  ```
- Terminal 2

  ```
  rosrun gesturebot dual_gesture.py  [For both hands]
  rosrun gesturebot left.py [for left hand]
  rosrun gesturebot right.py [for right hand]
  ```
  Keep Your Hand within the range of camera in-order to initiate the script depending on the script respectively. Ensure to have a different solid colored background.
  
- Terminal 3

  ```
  roscd gesturebot/scripts
  python ros_voice_control.py
  ```
## Measures of Success

<TABLE>
<TR>
	<TH>Measure of Success (from your PROPOSAL)</TH>
	<TH>Status (completion percentage)</TH>
</TR>
<TR>
	<TD> Webcam picks up Hand gestures from the camera and displays them

</TD>
	<TD>100%</TD>
</TR>
<TR>
	<TD>Convert the gestures to numerical values or words and print them</TD>
	<TD>100%</TD>
</TR>

<TR>
	<TD> Send information to the turtlebot so it understands how to move</TD>
	<TD>100%</TD>
</TR>

<TR>
	<TD>World Creation to navigate the turltebot</TD>
	<TD>100% </TD>
</TR>
<TR>
	<TD>  add in voice commands </TD>
	<TD>100% [The code from provided resources can run parallelly with hand gesture scripts]</TD>
</TR>

</TABLE>

---

## What did you learn from this project?

Through this project we learned how to not just use the camera on the robot but also to use the camera that is on the device running the code. this allows us to physically communicate to the robot by using our hand. we also learned how to implement voice recognition to achieve further communication. 
As we went through the project we were able to create region of interest so that the camera on the device running the code only looks for items in that region. We learned how to take the images from the main image and defined a  region to create a binary mask by providing skin color range from HSV values. In this mask we were able to set up a code that would count the number of defects in the item it is looking at. For example, if you hold up 2 fingers it does count the 2 fingers it counts the defect (valley between your fingers) which would be one in this case. After this we convert the numbers in to movement along the x-axis and z-axis using `twist()` commands. 


---

## Future Work

We have successfully implemented simple hand gestures to navigate the turtlebot around a map/maze/world. Future scope of this project includes :

- Improved Skin tone detection.
- Developing a ML script to capture hand gestures even more accurately. The resource link for this is:
 https://www.youtube.com/watch?v=Y6oLbRKwmPk
- Integrating hand and voice gesture into a single script with more definitive commands.
- Also implement the obstacle avoidance feature to safely stop the turtlebot in case of any command lag
- Using voice-based commands and odometry sensor, giving commands to the turtlebot to navigate around the map automatically.
- Using similar voice commands to find a specific item around the house using patrolbot concepts.


---

## References/Resources

- https://www.youtube.com/watch?v=cpwEV3bFYNg
	- Resource  for finding angle and defects from contours and drawing it on image.
- https://github.com/gorinars/ros_voice_control.git
	- Github repository for voice control script
- https://github.com/IE-482-582/fall2018.git     Chapter 9 redball code
	- Redball follow script to find contour from the image.
- https://docs.opencv.org/trunk/d9/d61/tutorial_py_morphological_ops.html
	- Morphological Transformations to make the mask as clear as possible for proper detection.
- Programming Robots with ROS by Morgan Quigley, Brian Gerkey, and William D. Smart





