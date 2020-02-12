ROS1 Host-Side Environment Setup Procedure
==========================================

Basic Information
-----------------
- Main OS Information:<br>
  Windows: Microsoft Windows [Version 10.0.19041.21] (Windows 10 Insider Preview SLOW Ring), XLaunch Installed
  Ubuntu: Windows Subsystem for Linux <b>Version 2</b>, Ubuntu 18.04
- Assuming reader knows how to use Ubuntu(linux) BASH Term.

Ubuntu Basic Setup
------------------
We need to change ubuntu APT Source server<br>
Open VIM Editor by below command;
```
$ vim /etc/apt/sources.list
```
in VIM Page, execute this command(before this, press ESC key):
```
%s/archive.ubuntu.com/mirror.kakao.com
```
Save it, and hop out of VIM by executing :w, :q.<br><br>
Update source cache and repository / Upgrade system package by:
```
$ sudo apt-get update && sudo apt-get upgrade
```

ROS1 Setup
----------
This step will install basic ROS1 package(catkin, default-basic package.)
execute:
```
$ cd ~
$ wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_melodic.sh
$ chmod 777 install_ros_melodic.sh
$ ./install_ros_melodic.sh
```
After command execution, it should prompt
"[Complete!!!]", otherwise, it caused error and failed to install ROS1 Melodic.

ROS1 Additional Package setup.
------------------------------
This will install ROS1 additional package - something like teleop, navigation, etc.<br>

Open Terminal, and execute the following.
```
$ sudo apt-get install -y ros-melodic-joy ros-melodic-teleop-twist-joy ros-melodic-teleop-twist-keyboard ros-melodic-laser-proc ros-melodic-rgbd-launch ros-melodic-depthimage-to-laserscan ros-melodic-rosserial-arduino ros-melodic-rosserial-python ros-melodic-rosserial-server ros-melodic-rosserial-client ros-melodic-rosserial-msgs ros-melodic-amcl ros-melodic-map-server ros-melodic-move-base ros-melodic-urdf ros-melodic-xacro ros-melodic-compressed-image-transport ros-melodic-rqt-image-view ros-melodic-gmapping ros-melodic-navigation ros-melodic-interactive-markers
```
After executing above command, we have to build some additional driver and packages to ~/catkin_ws in order to make TB3 run.(TB3 Bringup, LDS Driver, etc)<br>
Execute the following commands.
```
$ cd ~/catkin_ws/src/
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
$ cd ~/catkin_ws && catkin_make -j4
```
After this, execute:
```
$ echo "source ~/catkin_ws/devel/local_setup.bash" >> ~/.bashrc
```
This command will enable package we that we built just before.

ETC: Adding Packages to catkin_ws and enabling it.
--------------------------------------------------
This will show you how to add additional packages to catkin_ws and enable it.
1. Clone source repository to ~/catkin_ws/src
2. cd to ~/catkin_ws
3. execute: catkin_make -j(maximum thread supported by host/target OS)<br>
for me, I execute catkin_make -j12.
