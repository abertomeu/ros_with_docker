<div id="top"></div>

# ROS with DOCKER
This repository has been created to store basic examples for using ROS in Docker.

***
***
## Templates:
These examples have been tested on:
- PC with an **Nvidia GeForce RTX 2080** graphics card for the dockers in the folder [NVIDIA](./nvidia/).
- Laptop with integrated graphics card **Intel Iris Plus Graphics** for the dockers in the folder [INTEGRATED](./integrated/)

Dockers from *INTEGRATED* folder does not launch a Gazebo environment.

To run the containers, you need to go to the corresponding folder of the image you want to launch and run:
```
sudo docker-compose up --build -d
sudo docker-compose up -d
```
The first command compiles the image (*--build*) and launches the containers (*up*) in the background (*-d*). The second one directly launches the containers (*up*) in the background (*-d*).

Once the containers are launched, to access any of them, run:
```
sudo docker exec -it <ContainerID> bash
```
It executes an interactive terminal (*-it*) in the corresponding container with a shell (*bash*).

Once inside the container, to be able to run commands like *rostopic list*, you need to configure the ROS environment variables:
```
source /opt/ros/<distro>/setup.bash
```

If we only want to visualize the logs of the container, execute:
```
sudo docker logs <ContainerID>
```

To stop a specifi container, run the following command:
```
sudo docker stop <ContainerID>
```

And, to run it again:
```
sudo docker run <ContainerID>
```

To remove the containers, run the following command:
```
sudo docker-compose down
```

**Important!!:** Before launching any container, execute the following command from the terminal so that Docker can connect to the X11 server:
```
xhost +local:docker &> /dev/null
```

***
***
### **Kinetic Docker**:
This Docker image is based on the osrf/ros:kinetic-desktop-full tag.

It launches a ROS master, the talker and listener nodes from rospy_tutorials, rqt_graph, RViz, and Gazebo (Only in *NVIDIA* Docker).

* *NVIDIA* Docker: Unlike melodic and noetic Dockers, it requires a specific [Dockerfile](./nvidia/kinetic/ros-kinetic-gui/Dockerfile) configuration for the visual part since it does not contain the necessary openGL configuration for the visualization of Gazebo.

***

### **Melodic Docker**:
This Docker image is based on the osrf/ros:melodic-desktop-full tag.

It launches a ROS master, the talker and listener nodes from rospy_tutorials, rqt_graph, RViz, and Gazebo (Only in *NVIDIA* Docker).

***

### **Noetic Docker**:
This Docker image is based on the osrf/ros:noetic-desktop-full tag.

It launches a ROS master, the talker and listener nodes from rospy_tutorials, rqt_graph, RViz, and Gazebo (Only in *NVIDIA* Docker). 

***

### **Scara Robot Docker**:
This Docker is based on the osrf/ros:melodic-desktop-full tag.

It launches a package called robot_scara. This package contains two launch files:
* rviz_scara.launch: It generates a 4-DoFs SCARA robot with a gripper. Additionally, it is visualized using *Rviz* and can be manipulated using *rqt_joint_state_publisher*.
* spawn_scara.launch: The package launches a SCARA robot with 4-DoFs and a gripper. The robot is simulated in *Gazebo* and visualized in *Rviz*. Additionally, by entering the *robot-scara* container, it can be used the command *rosrun rqt_joint_trajectory_controller rqt_joint_trajectory_controller* to easily control the robot in *Gazebo*.

The container from *NVIDIA* folder executes the *spawn_scara.launch* file, and from *INTEGRATED* the *rviz_scara.launch*.

In addition, this container shares the folder *./robot-scara/robot_scara* to folder */root/catkin_ws/src/robot_scara* of the container. This allows us to modify the package from outside the container and the changes take effect inside it.

***
***

## Useful commands for Docker

```
sudo docker pull <tag:image>
sudo docker ps
sudo docker ps -a
sudo docker logs <ContainerID>
sudo docker exec -it <ContainerID> /bin/bash
sudo docker exec -it <ContainerID> bash

sudo docker run <ContainerID>
sudo docker stop <ContainerID>

sudo docker-compose up --build -d
sudo docker-compose up -d
sudo docker-compose down
```
***


<div align="center">
  <a>
    <img src="./docker_main.png" alt="Logo" height="200">
  </a>
</div>

***

## References:
* [http://wiki.ros.org/docker/Tutorials/Compose](http://wiki.ros.org/docker/Tutorials/Compose)
* [https://wiki.ros.org/docker/Tutorials/GUI](https://wiki.ros.org/docker/Tutorials/GUI)
* [https://github.com/koenlek/docker_ros_nvidia](https://github.com/koenlek/docker_ros_nvidia)
* [https://github.com/turlucode/ros-docker-gui.git](https://github.com/turlucode/ros-docker-gui.git)

<p align="right">(<a href="#top"> TOP </a>)</p>