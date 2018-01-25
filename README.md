The dwl-lcmtypes
==============================================

## <img align="center" height="20" src="https://i.imgur.com/vAYeCzC.png"/> Introduction

The Lightweight Communications and Marshalling (LCM) is a libraries with a set of tools for message passing and data marshalling, targeted at real-time systems where high-bandwidth and low latency are critical. It provides a publish/subscribe message passing model and automatic marshalling/unmarshalling code generation with bindings for applications in a variety of programming languages. For more information you can see: https://lcm-proj.github.io/

The Dynamic Whole Body Locomotion library (DWL) describes a set of core functions targeted to developed, design, and deploy locomotion algorithms, i.e. planning, control, etc. DWL is core library used in many projects of the Dynamic Legged Systems Lab of Istituto Italiano di Tecnologia (for more details about the project see http://www.iit.it/en/advr-labs/dynamic-legged-systems.html). For more details about DWL software infrastructure please visit https://github.com/robot-locomotion/dwl.

The dwl_lcmtypes are a set of message description which are compatible with DWL standards. This allows us to define the standarized messages of DWL in  LCM.

| [![](https://i.imgur.com/BT7fRCU.gif)](https://www.youtube.com/watch?v=ENHvCGrnr2g&t=2s) | [![](https://i.imgur.com/4kKhryj.gif)](https://www.youtube.com/watch?v=KI9x1GZWRwE)
|:-------------------------:|:-------------------------:|
| [![](https://i.imgur.com/yXTtxUK.gif)](https://www.youtube.com/watch?v=ArV2yh7KSfE) | [![](https://i.imgur.com/RKe3sNo.gif)](https://www.youtube.com/watch?v=KI9x1GZWRwE)
|||

The source code is released under a [BSD 3-Clause license](LICENSE).

**Author: Carlos Mastalli, carlos.mastalli@laas.fr<br />
With support from the Dynamic Legged Systems lab at Istituto Italiano di Tecnologia<br />**


## <img align="center" height="20" src="https://i.imgur.com/fjS3xIe.png"/> Dependencies

The algorithms are built primarily in C/C++. The library uses a number of the local dependencies, which some of them are optionals.

The dwl-lcmtypes is a ROS packages with the following required dependencies:
* [CMake](http://www.cmake.org) (version 2.8.3 or higher)
* [DWL](https://github.com/robot-locomotion/dwl)
* [lcm](https://github.com/lcm-proj/lcm)


## <img align="center" height="20" src="https://i.imgur.com/x1morBF.png"/> Building

Before building the dwl_lcmtypes you need to install the dependencies of DWL. Additionally you have to build dwl with catkin.

The dwl_rviz_plugin is a catkin project which can be built as:

	cd your_ros_ws/
	catkin_make
