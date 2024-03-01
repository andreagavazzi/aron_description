# aron_description

## Overview
This package contains the URDFs and meshes for Aron. The STL files are located in the [meshes](meshes/) directory. Next, the URDFs for the robot are located in the [urdf](urdf/) directory. They are written in 'xacro' format so that users have the ability to customize what parts of the URDF get loaded to the parameter server (see the 'Usage' section below for details). Note that all the other ROS packages in the sub-repo reference this package to launch the robot model.

## Structure

<img align="right" src="https://github.com/andreagavazzi/aron_description/blob/main/aron_description.png"/>

This package contains the [aron_description.launch](launch/aron_description.launch) file responsible for loading the robot model. It launches up to four nodes as described below:
- **robot_state_publisher** - uses the URDF specified by the parameter robot_description and the joint positions from the joint_states topic to calculate the forward kinematics of the robot and publish the results via tf.
- **joint_state_publisher** - responsible for parsing the 'robot_description' parameter to find all non-fixed joints and publish a JointState message with those joints defined.
- **joint_state_publisher_gui** - does the same thing as the 'joint_state_publisher' node but with a GUI that allows a user to easily manipulate the joints.
- **rviz** - displays the virtual robot model using the transforms in the 'tf' topic.

## Usage
To run this package, type the line below in a terminal:
```
$ roslaunch aron_description aron_description.launch use_joint_pub_gui:=true
```
This is the bare minimum needed to get up and running. Take a look at the table below to see how to further customize with other launch file arguments.

| Argument | Description | Default Value |
| -------- | ----------- | :-----------: |
| robot_name | name of the robot (typically equal to `aron`, but could be anything) | 'aron' |
| base_link_frame | name of the 'root' link on the turret; typically 'base_link', but can be changed if attaching the turret to a mobile base that already has a 'base_link' frame| 'base_link' |
| use_world_frame | set this to true if you would like to load a 'world' frame to the 'robot_description' parameter which is located exactly at the 'base_link' frame of the robot; if using multiple robots or if you would like to attach the 'base_link' frame of the robot to a different frame, set this to false | true |  
| use_joint_pub | launches the joint_state_publisher node | false |
| use_joint_pub_gui | launches the joint_state_publisher GUI | false |
| use_rviz | launches Rviz | true |
| rvizconfig | file path to the config file Rviz should load | 'rviz/aron_description.rviz' |
| model | file path to the robot-specific URDF including arguments to be passed in | 'urdf/aron.urdf.xacro' |

## 3D Interactive view
Click on the view to rotate  

[![3D Interactive Model](https://github.com/andreagavazzi/aron_robot/blob/main/pics/Aron3d.png)](https://collaborate.shapr3d.com/v/N6kiM8O_q4no-M4yc836B)
