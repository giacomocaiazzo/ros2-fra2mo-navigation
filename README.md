# ROS 2 Fra2Mo Navigation and Mapping

**Contributors:** Marco Bartone, Giacomo Caiazzo, Matteo De Simone and Nicola Monetti.

### Overview
A ROS 2 workspace for simulating the Fra2Mo mobile robot in Gazebo and visualizing its navigation in RViz2. It includes Nav2 navigation, map exploration and saving, waypoint following, and ArUco marker detection with world-frame pose estimation.

### Usage

Open the terminal, open the container and enter into the directory where you want to download the folder, then download it with:

	git clone https://github.com/giacomocaiazzo/Giacomo_Caiazzo_Homework_4
 
To build the packages, enter into the ROS2 workspace and build them with:

	colcon build

After this, use the source command:

	source install/setup.bash

--------------------------------

To load the world with leonardo_race_field and the mobile robot, run the simulation on Gazebo with:

	ros2 launch rl_fra2mo_description gazebo_fra2mo.launch.py

To launch the nav2_bringup node, open another terminal and use the following command:

	ros2 launch rl_fra2mo_description fra2mo_explore.launch.py

After this, open another terminal and use the following command to make the mobile robot follow a trajectory:
  
	ros2 run rl_fra2mo_description follow_waypoints.py

It's possible to select between two different arguments, each associated with a different path:

-  "map_explore", to explore the map, useful to save it;

-  "goals", to follow a set of points in the world map.

To save the map after the robot has explored the map successfully, use the following command in the ROS2 workspace on a different terminal:

	ros2 run nav2_map_server map_saver_cli -f <map_name>

--------------------------------

To make the robot look for and detect the aruco marker, use the following commands in the ROS2 workspace *in two different terminals*:

	ros2 launch rl_fra2mo_description fra2mo_aruco.launch.py
and:

	ros2 run rl_fra2mo_description aruco_finder.py
 The aruco pose estimation in world frame can bee read from the /tf_static topic using:

  	ros2 topic echo /tf_static 
--------------------------------

To launch RVIZ2 with the desired configuration use the following commands:

-To use slam_view.rviz configuration file:

	ros2 launch rl_fra2mo_description display_fra2mo.launch.py use_slam_view:=true

-To use explore.rviz configuration file:

	ros2 launch rl_fra2mo_description display_fra2mo.launch.py use_explore:=true

-else to run empty RVIZ2 run:

	ros2 launch rl_fra2mo_description display_fra2mo.launch.py

