# Mobile Robot Controller

This repository contains the `bumperbot_controller` package for ROS 2, which includes a waypoint navigation system and a velocity controller. The package also includes a differential kinematics calculation based on wheel encoder values.

## Installation

Clone this repository into your ROS 2 workspace and build:

```sh
cd ~/ros2_ws/src
git clone <repository_url>
cd ~/ros2_ws
colcon build
source install/setup.bash
```

## Running the Package

### 1. Launching the Controller

The velocity controller can be launched using:

```sh
ros2 launch bumperbot_controller controller.launch.py
```

This will:
- Start the velocity controller.
- Publish the odometry frame.
- Compute differential kinematics from wheel encoder values using `/joint_states`.

#### Parameters
You can provide the necessary arguments like wheelbase, max RPM, and wheel radius:

```sh
ros2 launch bumperbot_controller controller.launch.py wheelbase:=0.5 max_rpm:=150 wheel_radius:=0.11
```

### 2. Running Waypoint Navigation

The waypoint navigation script can be executed using:

```sh
ros2 run bumperbot_controller waypoint_navigation.py
```

To provide specific waypoints as arguments:

```sh
ros2 run bumperbot_controller waypoint_navigation.py --ros-args -p waypoint_1_x:=20.0
```

## Additional Notes

- Ensure all dependencies are installed before running the package.
- Modify the parameters according to your robot’s specifications.
- Test in a simulation environment before deploying on hardware.

##Challenges
- I am not able to correctly navigate to 2nd location there is some error.
