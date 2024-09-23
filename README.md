# LIO_RF: LiDAR-Inertial Odometry and Localization with ROS2

Follow the instructions below to set up your environment, build the required workspace, and run the mapping and localization processes.

## Prerequisites

Before starting, ensure that you have installed the following dependencies:

### 1. Install ROS2
Follow the official [ROS2 installation guide](https://docs.ros.org/en/humble/Installation.html) for your platform.

### 2. Install GTSAM

LIO_RF requires the **GTSAM** (Georgia Tech Smoothing and Mapping) library. Install it using the following commands:

```bash
sudo add-apt-repository ppa:borglab/gtsam-release-4.2
sudo apt install libgtsam-dev libgtsam-unstable-dev
```

### 3. Create a ROS2 Workspace

Set up your ROS2 workspace for LIO_RF by following these steps:

```bash
mkdir -p ~/lio_ws/src
cd ~/lio_ws/src
git clone https://github.com/Onicc/liorf.git
git clone https://github.com/Onicc/liorf_localization.git
cd ../
colcon build
```

Your ROS2 workspace is now set up and ready for use.

## Activating the Workspace

After building the workspace, you need to activate the ROS2 environment:

```bash
cd ~/lio_ws
source install/setup.bash
```

## Running the Mapping and Localization Process

### 1. Build the Map

To begin building a map, launch the necessary ROS2 launch files:

```bash
ros2 launch liorf run_lio_sam.launch.py
```

To play back recorded data for map building, use:

```bash
ros2 bag play <bag_file>
```

### 2. Save the Map

Once the map is built, you can save it using the following ROS2 service call. This allows you to specify the resolution and destination path for the saved map:

```bash
ros2 service call /liorf/save_map liorf/srv/SaveMap "{resolution: 0.2, destination: /Documents/LOAM}"
```

Make sure to replace `/Documents/LOAM` with your preferred save path.

> **Note:** Paths are relative to your home directory.

### 3. Localization

For localization, launch the localization process:

```bash
ros2 launch liorf_localization run_localization.launch.py
```

## Notes

- Always ensure that the ROS2 environment is activated by running `source install/setup.bash` before using any ROS2 commands.
- Verify that the file paths for saving maps and playing bag files are correct.
