# Autonomous-racing
# ENPM690: Robot Learning Final Project

## Team Members

| Name             | UID       |
|------------------|-----------|
| Sameer Arjun S   | 119385876 |
| Jay Prajapati    | 119208625 |

## Prerequisites

- ROS Noetic
- Gazebo
- Ubuntu 20.04

## Using Docker for ROS Noetic and Gazebo

To run the ROS Noetic and Gazebo environments inside a Docker container, follow these steps:

### Setup

1. **Pull the ROS Noetic Docker image**

    ```bash
    docker pull ros:noetic-robot
    ```

2. **Run a Docker container**

    This command runs a Docker container with Gazebo and ROS Noetic, forwarding the display for GUI applications:

    ```bash
    docker run -it --name ros-gazebo -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --privileged ros:noetic-robot
    ```

3. **Build the Project**

    Inside the Docker container, follow these steps to set up the autonomous driving package:

    ```bash
    cd autonomous_driving
    rosdep install --from-paths src --ignore-src -r -y
    catkin_make
    ```

## Running the Project without Docker

If you have installed ROS Noetic natively on Ubuntu 20.04, follow these instructions:

1. **Prepare the Workspace**

    Copy the `autonomous_driving` folder into your ROS workspace.

    ```bash
    cd catkin_ws/src
    cp -r path/to/autonomous_driving .
    ```

2. **Simulation Setup**

    Run the PyGame simulation to record the best lap coordinates:

    ```bash
    cd autonomous_driving/scripts/sim
    python3 race.py
    ```

    After completion, copy the desired coordinates from the generated text file into the `scripts/data.py` file.

3. **Build the Workspace**

    Navigate back to the root of your ROS workspace to build the project:

    ```bash
    cd ~/catkin_ws
    catkin_make
    source devel/setup.bash
    ```

4. **Launch the Simulation**

    Start the Gazebo simulation with the following command:

    ```bash
    roslaunch autonomous_driving racing.launch
    ```

5. **Run the Autonomous Driving Script**

    In a new terminal, execute the robot control script:

    ```bash
    cd ~/catkin_ws/src/autonomous_driving/scripts/sim
    python3 run_robot.py
    ```

## Additional Resources

- Ensure the TurtleBot simulation package is installed. For installation details, refer to the [TurtleBot3 Quick Start Guide](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup).

