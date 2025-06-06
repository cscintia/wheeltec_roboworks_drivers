# `usb_cam_launcher` package for ROS2

This package is for easy use of the `usb_cam` package of ROS2. It provides a node that interfaces with USB cameras and publishes images as ROS2 topics.

## Quickstart

Assuming you have a supported ROS2 distro installed, run the following command to install the binary release:

```bash
sudo apt get install ros-<ros2-distro>-usb-cam
```

As of today this package should be available for binary installation on all active ROS2 distros.

If for some reason you cannot install the binaries, follow the directions below to compile from source.

## Running

The `usb_cam_node` can be ran with default settings, by setting specific parameters either via the command line or by loading in a parameters file.

We provide a "default" params file in the `usb_cam/config/params.yaml` directory to get you started. Feel free to modify this file as you wish.

Also provided is a launch file that should launch the `usb_cam_node_exe` executable along with an additional node that displays an image topic.

The commands to run each of these different ways of starting the node are shown below:

**NOTE: you only need to run ONE of the commands below to run the node**

```r
ros2 run usb_cam usb_cam_node_exe
```

```r
ros2 launch usb_cam_launcher usb_cam_a.launch.py
```

```r
ros2 launch usb_cam_launcher usb_cam_b.launch.py
```



run the executable while passing in parameters via a yaml file
```r
ros2 run usb_cam usb_cam_node_exe --ros-args --params-file /path/to/colcon_ws/src/usb_cam/config/params.yaml
```

To launch multiple nodes at once, simply remap the namespace of each one:

```
ros2 run usb_cam usb_cam_node_exe --remap __ns:=/usb_cam_0 --params-file /path/to/usb_cam/config/params_0.yaml
ros2 run usb_cam usb_cam_node_exe --remap __ns:=/usb_cam_1 --params-file /path/to/usb_cam/config/params_1.yaml
```


## Compression

Big thanks to [the `ros2_v4l2_camera` package](https://gitlab.com/boldhearts/ros2_v4l2_camera#usage-1) and their documentation on this topic.

The `usb_cam` should support compression by default since it uses `image_transport` to publish its images as long as the `image_transport_plugins` package is installed on your system. With the plugins installed the `usb_cam` package should publish a `compressed` topic automatically.

Unfortunately `rviz2` and `show_image.py` do not support visualizing the compressed images just yet so you will need to republish the compressed image downstream to uncompress it:

```
ros2 run image_transport republish compressed in/compressed:=image_raw/compressed raw out:=image_raw/uncompressed
```

#### Documentation

[Doxygen](http://docs.ros.org/indigo/api/usb_cam/html/) files can be found on the ROS wiki.

### License
usb_cam is released with a BSD license. For full terms and conditions, see the [LICENSE](LICENSE) file.

### Authors
See the [AUTHORS](AUTHORS.md) file for a full list of contributors.
