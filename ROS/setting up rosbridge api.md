# How to Setup ROSbridge WebSocket Server

This following the tutorial on the official website [here](http://wiki.ros.org/rosbridge_suite/Tutorials/RunningRosbridge).

## Setup

```bash
# install rosbridge
$ sudo apt-get install ros-<rosdistro>-rosbridge-suite

# source the ROS environment
$ source /opt/ros/<rosdistro>/setup.bash

# launch rosbridge
# this will create WebSocket server on port 9090
$ roslaunch rosbridge_server rosbridge_websocket.launch
```

`roslaunch` will automatically start roscore if it detects that it is not already running (unless the `--wait` argument is supplied)
```xml
<!-- To configure port number you need to set the ~/port parameter in ROS -->

<!-- this is an example launch file to run rosbridge on port 8080 -->
<launch>
  <include file="$(find rosbridge_server)/launch/rosbridge_websocket.launch"> 
     <arg name="port" value="8080"/>
  </include>
</launch>
```

This should have succcessfully started the ROS bridge, you can then start a ROS Node to run on the server 
