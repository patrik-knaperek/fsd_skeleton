# FSSIM installation manual

This is an installation manual for FSSIM alongside with fsd_skeleton environment developed by AMZ-Driverless FS team. For original documentation, see [AMZ_README](./AMZ_README.md). The original workspace has been utilized for purposes of STUBA Green Team Driverless.

## Prerequisities
 - Ubuntu 20.04
 - [ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu), Python 3
 - packages: `checkinstall, python3-catkin-tools, git`

## Install AMZ FSD skeleton
1. `$ cd <target_path>`
2. `$ git clone -b sgt-noetic-devel https://gitlab.com/sgt-driverless/simulation/fsd_skeleton.git`
3. `$ cd ./fsd_skeleton`
4. (`$ chmod +x update_dependencies.sh`)
5. `$ ./update_dependencies.sh`
6. `$ catkin build`
7. `Restart terminal`

## Install FSSIM
1. `$ cd <target_path>/fsd_skeleton/src`
2. `$ git clone -b sgt-noetic-devel https://gitlab.com/sgt-driverless/simulation/fssim.git`
3. `$ cd ./fssim`
4. `$ ./update_dependencies.sh`
6. `$ catkin config --no-blacklist`
7. `$ catkin build`
8. `$ FSD_source`

## Configuration
* cone detection characteristics: [sensors_1.yaml](./src/fssim_interface/fssim_config/sensors/sensors_1.yaml)
* speed: [pure_pursuit.yaml](./src/3_control/control_pure_pursuit/config/pure_pursuit.yaml)
* track selection: [local_simulation.yaml](./src/fssim_interface/fssim_config/local_simulation.yaml), [calibration_simulation.yaml](./src/fssim_interface/fssim_config/calibration_simulation.yaml)

## Launch FSSIM
1. `$ FSD_source`
2. `$ roslaunch fssim_interface fssim.launch` (may take more than a minute for the first time)

new terminal
1. `$ FSD_source`
2. `$ roslaunch control_meta trackdrive.launch`

launch for calibration: `$ roslaunch fssim_interface fssim_calibration.launch`

