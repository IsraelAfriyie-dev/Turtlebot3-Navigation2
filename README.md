# Turtlebot3-Navigation2
Turtlebot3 for Nav2(Notes)
The question is how do we make a robot navigate? the package used for the navogation is Nav2, and this saves us time for Robot to navigate
The Nav2 is the package that allows the robot to navigate form one point to another safely.
So in order to do this we will create a map with a SLAM. And the next step will be making sure the roboit navigate from point A to B.

To begin with we will install the packages:
 -sudo apt update
 -sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup ros-humble-turtlebot3*( This installs the nav2 package alongside with turtlebot3 packages) 

Start the trutlebot3 in a simulating environment and make sure it moves
specify which turlebot3 you need in your environement( Burger, waffle ... etc)
-gedit ~/.bashrc ( this opens the bashrc command and allow you to edit the turtlebot3 line of code) by adding... above the source.
-export TURTLEBOT3_MODEL=waffle

Use this to check 
-source .bashrc
-printenv | grep TURTLE ( it should print out:TURTLEBOT3_MODEL=waffle) for you to see the turtlebot3 type you are using.

We will start the gazebo app from the terminal.
-ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py

we will start a node that will make the robot move in Gazebo for a new terminal
-ros2 run turtlebot3_teleop teleop_keyboard 

Create a map with the SLAM
-ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True(This code launches the SLAM toolbox for turtlebot3 but it should be done alongisde ;launching of gazebo)
and this launces RVIZ software.
the goal is to generat ethe map from RVIZ window and save it

so terminal 1 start gazebo, terminal 2 start SLAM, and terminal 3 start teleop command to control the robot.
so as you move the robo, the map start to generate from SLAM

when you doen creating the map (open a new terminal to save it in your directory)
-israel@DESKTOP-61SQN9F:~$ mkdir map 
-ros2 run nav2_map_server map_saver_cli-f map/your_map (this creates the map, if error run the command mutlipe, times )
 (your_map.pgm  your_map.yaml) confirm that this exist in the directory. Now the map is saved.

stop all the runnning terminals
Now let the robot navigate in your map created
-start your robot( ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py)  
-open a new terminal to start the navogation for the robot (ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=map/your_map.yaml) stop and start again if you dont see the map

when the map launches then you have to give an estimation of where the robot is by referencing gazebo.( use 2D Pose Estimate by clicking to make the position)                
