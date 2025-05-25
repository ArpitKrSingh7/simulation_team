# Simulation Development

This repository contains Husarion_ws. This repo will help the image processing and Navigation team to implement there algos and other things properly , Basically a testing envirnoment.

## Current Development
- `components.yaml` : Added 4 Zed X camera as per mentioned in ERC Docx.
- `husarion_gz_worlds`: Custom Compressed Mars World simulation world with aruco markers and anomaly objects.
- `aruco_markers`, `aruco_markers_msgs`: ArUco marker detection.
- `stereolabs_zed.urdf.xacro` : Solved the pc2 vertical inverison thing , Optimized it further to support in medium range PCs.
- `gz_ros2_control` : Issue solved which was coming due to this particular thing.
- Differential dirve working fine while visualizing all 4 cam Pc2 data.
- Properly configured for Jazzy (Ubuntu 24.04).

## 🛠️ Let's Get Started

### Prerequisites

- ROS 2 Jazzy
- `gazebo Harmonic` : Visit [Gazebo Harmonic installition Guide](https://gazebosim.org/docs/harmonic/install_ubuntu/) to get the right thing for this package.
- opencv packages
  Download it through
  ``` bash
  sudo apt install libopencv-dev
  ```

### Intall Instructions
```
Install the Zip file , and extract it - remember it's a workspace
Remove the install , build and log from the husarion_ws directory
There will be a `bas.sh` file don't remove it
```

### Build Instructions

```bash
# I assume that you have already sourced your Ros2 and all
# Build workspace
export HUSARION_ROS_BUILD_TYPE=simulation

vcs import src < src/husarion_ugv_ros/husarion_ugv/${HUSARION_ROS_BUILD_TYPE}_deps.repos

sudo rosdep init
rosdep update --rosdistro $ROS_DISTRO
rosdep install --from-paths src -y -i

source /opt/ros/$ROS_DISTRO/setup.bash
colcon build --symlink-install --packages-up-to husarion_ugv --cmake-args -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF

source install/setup.bash

```
Previous Step will build the husarion related packages , now to build Aruco package follow these steps.

``` bash
# build the Aruco_markers_msgs package first
colcon build --packages-select aruco_markers_msgs

#Then build Aruco_makrers package
colcon build --packages-select aruco_markers

```

## Running Husarion Bot
``` bash
# To run the bot Enter this command
ros2 launch husarion_ugv_gazebo simulation.launch.py

```

After this thing for running the bot everytime , you can directly hit `./bas.sh` , it will rebuild the workspace + source it and run the bot automatically.

## Running Aruco Markers package 
- Follow my colleague [Harshini's](https://github.com/harshinisrisavitha/remote/blob/main/README.md) Repo.

### Extra Info
- `Ros2-devel` branch i used to build the husarion package.
- Sometimes you might get an error of joint state pubisher fialed to launch - This is common , just relaunch it several times.
- DICT_4X4_100 used in world. For aruco detection thing you can change the config file to detect other dictionaries as well.


## World 
This the Mars World 

![Mars World](https://github.com/user-attachments/assets/db2b18dc-3abc-43fb-9c08-aa3a6f536246)

## Rviz 
![Screenshot from 2025-05-18 12-45-14](https://github.com/user-attachments/assets/08cbd6b8-673a-4922-a5e2-3400595faee5)

## Aruco Detection and msg type 
Successfully detecting the Marker. 

![Screenshot from 2025-05-18 12-46-02](https://github.com/user-attachments/assets/276450b8-23d6-41e4-aa48-e8116a58e4b1)



A `MarkerArray` message is publish to the `/aruco/markers` topic

![Screenshot from 2025-05-18 12-51-38](https://github.com/user-attachments/assets/92db4d1f-5661-4ba3-a26b-fdeeafd318df)


Available dictionaries are 
```
DICT_4X4_50
DICT_4X4_100
DICT_4X4_250
DICT_4X4_1000
DICT_5X5_50
DICT_5X5_100
DICT_5X5_250
DICT_5X5_1000
DICT_6X6_50
DICT_6X6_100
DICT_6X6_250
DICT_6X6_1000
DICT_7X7_50
DICT_7X7_100
DICT_7X7_250
DICT_7X7_1000
DICT_ARUCO_ORIGINAL
DICT_APRILTAG_16h5
DICT_APRILTAG_25h9
DICT_APRILTAG_36h10
DICT_APRILTAG_36h11 
```












