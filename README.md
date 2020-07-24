# Nexus 4WD Mecanum Simulator
ROS Repository for the robot description and gazebo simulation of the 4WD Mecanum wheel robot from Nexus Robot: https://www.nexusrobot.com/product/4wd-mecanum-wheel-mobile-arduino-robotics-car-10011.html

<a href="url"><img src="/documentation/pictures/picture_1.png"></a>

**Disclaimer:**

I'm not affiliated in any way with Nexus Robotics. I just use one of their robot and wanted to write a Gazebo simulation for it. 

## Usage
Run the simulation for one nexus robot by using the following command line:

`roslaunch nexus_4wd_mecanum_gazebo  nexus_4wd_mecanum_world.launch `

To launch two nexus robots, use the following launch file:

`roslaunch nexus_4wd_mecanum_gazebo  nexus_4wd_mecanum_multi.launch `

## Dependencies
* Gazebo7 or Gazebo9
* robot_state_publisher
* urdf
* tf

## Packages
* nexus_4wd_mecanum_description
* nexus_4wd_mecanum_gazebo

## nexus_4wd_mecanum_description
  Robot model description packages. Includes the URDF and the meshes of the robot.
  
### Launch files
* **nexus_4wd_mecanum_description.launch:** Loads the nexus 4WD mecanum robot description parameter and the robot state publisher.

* **nexus_4wd_mecanum_rviz.launch:** Loads the nexus 4WD mecanum robot description parameter and a RViz session.

## nexus_4wd_mecanum_gazebo
  Includes Gazebo plugin for simulating a velocity controller and launch files for running the simulation.
  
### Launch files
* **nexus_4wd_mecanum_world.launch:** Launches Gazebo and spawn one nexus robot.

     - **`use_sim_time`** Tells ROS nodes asking for time to get the Gazebo-published simulation time, published over the ROS topic /clock. Default: `true`.
     
     - **`gui`** Launch the user interface window of Gazebo. Default: `true`.
     
     - **`headless`** Enable gazebo state log recording. Default: `false`.

* **nexus_4wd_mecanum_multi.launch:** Launches Gazebo and spawn two nexus robots with their namespace. This launch file aims to provide an example for multi-robot simulation.

     - **`use_sim_time`** Tells ROS nodes asking for time to get the Gazebo-published simulation time, published over the ROS topic /clock. Default: `true`.
     
     - **`gui`** Launch the user interface window of Gazebo. Default: `true`.
     
     - **`headless`** Enable gazebo state log recording. Default: `false`.


* **spawn_one_nexus_4wd_mecanum.launch:** To be included in a launch file to spawn a nexus robot.

     - **`robot_name`** Robot name used as namespace for the spawned robot. Default: `nexus0`.
     
     - **`pose_x`** x coordinate (in m) of the robot spawn pose. Default: `0`.
     
     - **`pose_y`** y coordinate (in m) of the robot spawn pose. Default: `0`.


### Gazebo plugin
* nexus_ros_force_based_move:

  Outputs a force and a torque on the base link of a robot, using a velocity command as input and a proportional controller. Includes check for both Gazebo7 and Gazebo9 compatibility.

	* **Subscribed topic**
		* `/cmd_vel` (`geometry_msgs/Twist`)

		  Receives velocity command as a Twist message. The plugin will only process the linear velocity on the x and y-axis and the angular velocity on the z-axis

	* **Published Topics**
		 * `/odom` (`nav_msgs/Odometry`)
		
	  	  	Odometry from Gazebo model pose and velocity.
		  
		 *  `/front_sensor` (`sensor_msgs/Range`)
		
	  		Front ultrasonic range sensor distance
		
	 	*  `/left_sensor` (`sensor_msgs/Range`)
		
	  		Left ultrasonic range sensor distance
		
	 	*  `/rear_sensor` (`sensor_msgs/Range`)
		
	  		Rear ultrasonic range sensor distance
		
	 	*  `/right_sensor` (`sensor_msgs/Range`)
		
	  		Right ultrasonic range sensor distance

## To do
* Add wheel velocity controller (only for visual feedback)
