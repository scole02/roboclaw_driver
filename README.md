## RAT ROS WS
Works with ROS Noetic and Python3

Installing ROS Noetic on Ubuntu20.04/Debian10 X86 is quite easy, and can be done with apt 

For 32 Bit RPI all packages must be built on machine :/ I have one workspace with my desktop install
and all the additonal package dependencies for this repo (ros_catkin_ws) and this repo with the custom
code. Not sure if combining these will be easier? It would eliminate the need to install to /opt/ros/noetic though.


Links:  
  [RPi OS Buster Noetic Desktop Install](https://projects-raspberry.com/lidar-integration-with-ros-noetic-on-raspberry-pi-os/)  
  [Adding a Package to a workspace](http://wiki.ros.org/rosinstall_generator) (section 4.5 is helpful)
  
Packages to be added that are not included in desktop install:

- ros_control
- ros_control_boilerplate  
- moveIt?  


### Adding New Packages 
*Assuming your workspace was made with Desktop Install Instructions above*
1. Bring packages into isolated workspace src directory  
 `$ cd ~/my_ros_install_ws`  
 `$ rosinstall_generator PKG_NAME --rosdistro noetic --deps | vcs import src` 
   
2. Build/Install said package  
  `sudo src/catkin/bin/catkin_make_isolated --only-pkg-with-deps ros_control_boilerplate --install -DCMAKE_BUILD_TYPE=Release --install-space /opt/ros/noetic -DPYTHON_EXECUTABLE=/usr/bin/python3`

### Quirks
- When building `ros_control_boilerplate` there may be an error finding the `gflags` library, in my case it was not installed on Ubuntu 20.04 or RPi OS Buster. Use: `sudo apt install libgflags-dev`
