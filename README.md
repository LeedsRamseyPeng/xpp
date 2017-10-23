# XPP
![Logo](doc/logo.jpg)

Xpp is a package for the visualization of motion plans for legged robots. Apart from drawing support areas, contact forces and motion trajectories in RVIZ, it also displays these plans for specific robots. Current robots include:

- [HyQ] - Italian Institute of Technology

The source code is released under a [BSD 3-Clause license](ros_package_template/LICENSE).

**Author: [Alexander W. Winkler](https://awinkler.github.io/)  
Maintainer: [Alexander W. Winkler](https://awinkler.github.io/)  
Affiliation: [Robotics Systems Lab](http://www.rsl.ethz.ch/), ETH Zurich**

See the [list of contributors](AUTHORS.txt) for further contributors.

[![Build Status](https://ci.leggedrobotics.com/buildStatus/icon?job=github_leggedrobotics/xpp/master)](https://ci.leggedrobotics.com/job/github_leggedrobotics/job/xpp/job/master/)


### Dependencies

- [ROS] (middleware for robotics)
   Packages: catkin, roscpp, tf, kdl_parser, robot_state_publisher, message_runtime, message_generation, std_msgs, geometry_msgs, sensor_msgs, rviz, rosbag
      
      sudo apt-get install ros-[ros_distro_name]-[pkg_name]
 
- [Eigen] (linear algebra library)

      sudo apt-get install libeigen3-dev

#### Building

To build from source, clone the latest version from this repository into your catkin workspace and compile the package using

    cd catkin_workspace/src
    git clone https://github.com/legged_robotics/xpp.git
    cd ..
    catkin_make -DCMAKE_BUILD_TYPE=Release


### Unit Tests

Make sure everything installed correctly by running the unit tests through

    catkin_make run_tests
    
or if you are using [catkin tools].

    catkin build xpp_vis --no-deps --verbose --catkin-make-args run_tests

### Usage

A few examples for different robots are provided in the `xpp_examples` package. For starters, run

    roslaunch xpp_examples monoped_ex_bag.launch  // or biped_ex.launch, hyq_ex.launch

These scripts actually executes the following steps:

1. Start the visualization nodes, launch rviz with the correct config and wait for robot messages using `roslaunch xpp_vis xpp_vis.launch`.
 
2. Now robot messages of type `xpp_msgs/RobotStateCartesian.msg` can be sent and visualized. Since we also want to display the URDF of a specific robot, the URDF file of the robot (e.g `monoped_description)/urdf/monoped.urdf` must be uploaded to the ROS parameter server.
  
3. Next a node must be created that transforms `xpp_msgs/RobotStateJoints.msg` into rviz TFs. If we also want to display Cartesian messages `xpp_msgs/RobotStateCartesian.msg`, Inverse Kinematics are neccessary for the specific robots.
 
4. Finally, motions plans must be published for the specific robots. Rosbags of sample motions plans can be found at `xpp_examples/bags/` and can be run using `rosbag play`. To see some examples of how to generate these
bag files or messages, check out `xpp_examples/src/monoped_bag_builder.cc` and `xpp_examples/src/monoped_publisher.cc`.

### Publications

If you use this work in an academic context, please cite the following publication(s):

A. Winkler, F. Farshidian, D. Pardo, M. Neunert, and B. Jonas: **Fast Trajectory Optimization for Legged Robots using Vertex-based ZMP Constraints**. IEEE Robotics and Automation Letters (RA-L), 2017. ([PDF](http://dx.doi.org/10.1109/LRA.2017.2723931))

    @article{winkler17b,
        author    = {Winkler, Alexander W and 
                     Farshidian, Farbod and 
                     Pardo, Diego and 
                     Neunert, Michael and 
                     Buchli, Jonas},
        title     = {Fast Trajectory Optimization for Legged Robots 
                     using Vertex-based ZMP Constraints},
        journal   = {IEEE Robotics and Automation Letters (RA-L)},
        year      = {2017},
        month     = {oct},
        pages     = {2201-2208},
        doi       = {10.1109/LRA.2017.2723931},


### Bugs & Feature Requests

Please report bugs and request features using the [Issue Tracker](https://github.com/leggedrobotics/xpp/issues).

[HyQ]: https://www.iit.it/research/lines/dynamic-legged-systems
[ROS]: http://www.ros.org
[rviz]: http://wiki.ros.org/rviz
[catkin tools]: http://catkin-tools.readthedocs.org/
[Eigen]: http://eigen.tuxfamily.org