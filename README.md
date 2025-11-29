# turtlebot3
sudo apt update
sudo apt install gazebo
gazebo --version
gazebo
Install TurtleBot3 Simulation Packages
sudo apt update
sudo apt install ros-humble-turtlebot3 ros-humble-turtlebot3-simulations
mkdir -p ~/turtlebot3_ws/src
cd ~/turtlebot3_ws/src
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3.git
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cd ~/turtlebot3_ws
colcon build --symlink-install
source install/setup.bash
Set TurtleBot3 Model
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc
colcon build --symlink-install
Launch TurtleBot3 Simulation in Gazebo
Start gazebo simulations:
source /opt/ros/humble/setup.bash
ros2 launch turtlebot3_gazebo empty_world.launch.py
Move the Robot (Keyboard Teleop)
source /opt/ros/humble/setup.bash
ros2 run turtlebot3_teleop teleop_keyboard
Troubleshooting Common Issues
● Gazebo Development Packages Not Found
If you try building TurtleBot3 from source, Ubuntu 22.04 does not provide libgazebo11-dev.
Use the apt method to install TurtleBot3.
● Package Not Found Errors
If launching fails with package not found, ensure correct apt install, environment
variables, and ROS workspace sourcing.
● Workspace Build Issues
Clean build with:
● bash
rm -rf build install log
colcon build --symlink-install
●
● Setting Model Variable
Always make sure TURTLEBOT3_MODEL is exported and sourced by the shell.
7. Optional: Fresh Workspace Reset
Remove All Files
bash
rm -rf ~/turtlebot3_ws
Remove Apt Packages
bash
sudo apt remove --purge ros-humble-turtlebot3* -y
sudo apt autoremove -y
Then repeat the installation steps above.
Reference Commands
● Launch TurtleBot3 simulation:
● bash
ros2 launch turtlebot3_gazebo empty_world.launch.py
●
● Keyboard control:
● bash
ros2 run turtlebot3_teleop teleop_keyboard
●
● Set TurtleBot3 Model:
● bash
● export TURTLEBOT3_MODEL=burger
TurtleBot3 SLAM Simulation Guide
Prerequisites
 Install ROS 2 Humble (already done)
 Install Gazebo (already done)
 Install TurtleBot3 simulation packages:
sudo apt update
sudo apt install ros-humble-turtlebot3 ros-humble-turtlebot3-simulations -y
Set TurtleBot3 model
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc
Launch the Simulation World
Open Terminal 1 and launch a recommended world for SLAM:
TurtleBot3 World
source /opt/ros/humble/setup.bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
OR
TurtleBot3 House
source /opt/ros/humble/setup.bash
ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
Run the SLAM Node
Open Terminal 2. Start the Cartographer SLAM node:
source /opt/ros/humble/setup.bash
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_cartographer cartographer.launch.py
use_sim_time:=True
Start Teleoperation to Move the Robot
Open Terminal 3 and run keyboard teleop:
source /opt/ros/humble/setup.bash
export TURTLEBOT3_MODEL=burger
ros2 run turtlebot3_teleop teleop_keyboard
Save the Generated Map
Open Terminal 4 when mapping is complete:
source /opt/ros/humble/setup.bash
ros2 run nav2_map_server map_saver_cli -f ~/map
