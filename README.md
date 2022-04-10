# Hamster simulation
This is a gazebo simulation for the robot _"Hamster"_ by cogniteam. It is based on the offical simulation by cogniteam using ROS Hydro and was adapted to work with the newer distro ROS Noetic.
For more information see:
- Cogniteam's website: https://www.cogniteam.com/
- Wiki about cogniteam: https://wiki.cogni.io/Cogniteam
- Wiki about Hamster robot: https://wiki.cogni.io/Category:Hamster
- Wiki about Hamster simulation: https://wiki.cogni.io/Simulation

### Installation
1. Install Ubuntu 20.04.4 LTS (Focal Fossa): https://releases.ubuntu.com/20.04/
2. Install ROS (1) Noetic for Ubuntu:
    - http://wiki.ros.org/noetic/Installation/Ubuntu
    - Note: It's recommended to install `ros-noetic-desktop-full`, because it includes the necessary simulation packages. If either `ros-noetic-desktop` or `ros-noetic-ros-base` is chosen for installation instead, those have to be installed manually.
3. Install the following additional packages required by the simulation via `sudo apt install ros-noetic-<package_name>`
    - costmap-2d
    - ackermann-msgs
    - random-numbers
3. Clone the repo from _https://github.com/philippreinig/hamster_simulation_
4. Build the project by executing `catkin_make` in the root folder

### Launching the simulation
1. Navigate into the root folder of the project by using the `cd` command accordingly
2. Make sure you sourced the correct ros-distro and the project itself
    - `source /opt/ros/noetic/setup.bash`
    - `source devel/setup.bash`
2. Launch one of the available simulations
- Hamster without a depth camera: `roslaunch hamster_vehicle_gazebo hamster_V6_spawner.launch`
- Hamster with a depth camera: `roslaunch hamster_vehicle_gazebo hamster_V7_spawner.launch` 
- Two hamster robots: agent1 is a hamster V6, agent2 is a hamster V7: `roslaunch hamster_vehicle_gazebo hamster_multi_vehicle.launch`

### Visualizing sensor inputs using rviz
- NOTE: Hamster V6 does not have a depth camera!
- Launch rviz using the command `rviz`
- Add the according topics ro rviz using _Add_ -> _Add topic_
    - Camera image: _/agent1/camera/color/image_raw_ : _Image_
    - Camera depth image: _/agent1/camera/depth/image_raw_ : _Image_
    - Lidar: _/agent1/scan_ : _LaserScan_
- There are also two config files for each hamster version to visualize all sensor inputs at _rviz/_. They can be opened via _File_ -> _Open config_ in rviz.

### Known bugs
- The costmap is not being built using the sensor inputs - the reason couldn't be found.
- The path planning does not work because of the costmap not having any obstacles. The path planned is always straight ahead.
- The hupster wandering does not work because of the useless path planning. The Hamster robot will drive forward until it hits an obstacle which stops him.

