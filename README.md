# HaRoN
The goal of this educational project is to develop a rescue robot.

[![License](https://img.shields.io/github/license/ucuapps/robert.svg)](https://github.com/ucuapps/robert/blob/kinetic-devel/LICENSE)


## Docker
For convenience it is recommended to use Docker containers.
Please follow these steps to run Docker container on your machine.

 1. Install Desktop OS Ubuntu Trusty or Xenial on your machine or in virtual machine
 2. Install Docker-CE using these [instructions](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/)
 3. In order to executed Docker without sudo please execute
```bash
sudo usermod -aG docker $USER
```
 4. Logout and login to your machine again :)
 5. For development [the following](http://hub.docker.com/r/lyubomyrd/haron/) docker container was used.
 6. To pull it please run
```bash
docker pull lyubomyrd/haron:latest
```
 7. Use the following command to start Docker container
```bash
docker run -it --privileged --name haron_dev -p 8080:8080 -e DISPLAY -e LOCAL_USER_ID=$(id -u) -v /tmp/.X11-unix:/tmp/.X11-unix:rw lyubomyrd/haron:latest
```
 8. Black window of [Terminator](https://gnometerminator.blogspot.com/p/introduction.html) UI console will appear after some time.
 9. You can use it's features to [split terminal window](https://linux.die.net/man/1/terminator) into smaller terminals and run few commands in parallel (Ctrl+Shift+E).
 10. If you want to run real robot add user to dialout group and restart Docker container
```bash
sudo usermod -a -G dialout user
```

In order to relaunch docker container after you closed Terminator window or rebooted machine please run
```bash
docker start haron_dev
```
After some time Terminator window will reappear.

## IDEs

In case if you want to run PyCharm in Docker container please run

```bash
pycharm
```

To launch QtCreator please run

```bash
qtcreator
```

For VSCode type
```bash
vscode
```

# Designation:

The following designation will be used through the rest of the repository

Remote PC: R

Turtlebot(Raspberry): T

# Turtlebot start

Turtlebot is controller using ROS which is installed both on PC and Raspberry.

To execute the bringup sequence You have to perform the following steps:



## Steps that has to be performed inside the docker container's terminator window


1R) roscore

Connect to RPI (note that IP address might be different - this depends on network settings)

2R) ssh pi@192.168.43.216

(Password: turtlebot)

Now You have a separeate window inside the terminator that controlles Raspberry, therefore Tx notation corresponds to input into this window.

3T)  roslaunch turtlebot3_bringup turtlebot3_robot.launch

4R) roslaunch turtlebot3_bringup turtlebot3_remote.launch

# Teleoperation

1R) roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

# Mapping

Create a map:

1R) roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping

Save a map (do NOT close the previous window vefore the next step):

2R) rosrun map_server map_saver -f ~/map

After this step You can close 1R and 2R from mapping.

# Navigation

1R) roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml

# Active Slam packeges:
info available at https://github.com/hrnr/m-explore
Documentation for API: http://wiki.ros.org/explore_lite
1R) sudo apt install ros-${ROS_DISTRO}-explore-lite
2R) roslaunch explore_lite explore.launch
# Frontier explore package (one where you need define explore area by setting points manually):
https://github.com/paulbovbel/frontier_exploration/tree/melodic-devel/frontier_exploration
http://wiki.ros.org/frontier_exploration (guideline available there)

# Troubleshooting
See wiki for Troubleshooting
