# Formula Student Driverless Simulator (FSSIM)
___

© **AMZ Driverless**

**Authors:** Juraj Kabzan  
**Objective:** Test and simulate FS Driverless pipeline.
___

This workspace represents a complete driverless pipeline developed by FS team AMZ-Driverless (ETH Zurich). It contains a basic implementation of perception, estimation and control tasks. Thanks to `fssim` submodule, which simulates the physical environment of a Formula Student Driverless race track, the whole pipeline can be tested and visualized with Rviz. For original documentation, see [AMZ_README](./AMZ_README.md).

## FSSIM installation manual

This is an installation manual for FSSIM alongside with `fsd_skeleton` environment developed by AMZ-Driverless FS team. The original workspace has been utilized for purposes of STUBA Green Team Driverless.

### Prerequisities
 - Ubuntu 20.04
 - [ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu), Python 3
 - packages: `checkinstall, python3-catkin-tools, git`

### Install AMZ FSD skeleton
```sh
$ cd <target_path>
$ git clone --recurse-submodules https://gitlab.com/sgt-driverless/simulation/fsd_skeleton.git
$ cd ./fsd_skeleton
$ chmod +x update_dependencies.sh
$ ./update_dependencies.sh
$ catkin build
```
Restart terminal


### Install FSSIM
```sh
$ cd <target_path>/fsd_skeleton/src/fssim
$ ./update_dependencies.sh
$ catkin config --no-skiplist
$ catkin build
$ FSD_source
```
## Launch
### Configuration
* [sensors_1.yaml](./src/fssim_interface/fssim_config/sensors/sensors_1.yaml)
    - cone detection measurement characteristics
* [pure_pursuit.yaml](./src/3_control/control_pure_pursuit/config/pure_pursuit.yaml)
    - max speed (if using FSD control)
* [local_simulation.yaml](./src/fssim_interface/fssim_config/local_simulation.yaml), [calibration_simulation.yaml](./src/fssim_interface/fssim_config/calibration_simulation.yaml)
    - track selection
    - track check enable/disable
* [config.yaml](./src/fssim_interface/config/config.yaml)
    - control command source

### Launch FSSIM
```sh
$ FSD_source
$ roslaunch fssim_interface fssim.launch
```
_Note: Launching may take more than a minute for the first time._

Launch for calibration:
```sh
$ roslaunch fssim_interface fssim_calibration.launch
```

### Restart FSSIM
During launch, the most time-consuming element is Gazebo node. During testing, it is annoying to always terminate the whole `fssim.launch` and then wait until it loads again (in case we want to test new configuration). To avoid this, we add a shortcut - `reset_fssim` service.

By calling
```sh
$ rosservice call /fssim_interface/reset_fssim "{}"
```
it is possible to reset the car pose to the starting position and reload the Gazebo simulation while keeping the node running.

### Launch FSD control
```sh
$ FSD_source
$ roslaunch control_meta trackdrive.launch
```


