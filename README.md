# Technical Session: micro-ROS

This repository contains code demonstrated during the **technical session on micro-ROS**. It includes a simple ROS 2 Python publisher node and the corresponding micro-ROS Arduino subscriber node.



## Prerequisites

- ROS 2 (Humble)
- Arduino IDE (with micro-ROS library)
- Docker (for micro-ROS Agent)


## Running the ROS 2 Node (Publisher)

1. Create a new workspace:
   ```bash
   mkdir -p micro-ROS_ws/src
   cd micro-ROS_ws/src
   ```

2. Clone this repository into the `src` folder:
   ```bash
   git clone <this-repository-url> .
   ```

3. Build the workspace:
   ```bash
   cd ..
   colcon build --symlink-install
   ```

4. Source the workspace:
   ```bash
   source install/setup.bash
   ```



## Running the micro-ROS Node (Subscriber on Arduino)

1. Download the ZIP of this [**micro-ROS Arduino repository**](https://github.com/micro-ROS/micro_ros_arduino/tree/humble).

2. Open Arduino IDE → go to `Sketch > Include Library > Add .ZIP Library` and add the downloaded library.

3. Open `sub_micro-ROS.ino` from this repo in Arduino IDE.

4. Select the correct board and port, then upload the sketch.



## Running micro-ROS Agent (Serial Communication)

Use Docker to run the micro-ROS Agent via serial:
```bash
docker run -it --rm -v /dev:/dev --privileged --net=host \
  microros/micro-ros-agent:humble serial --dev [YOUR_BOARD_PORT] -v6
```

Replace `[YOUR_BOARD_PORT]` with the actual serial port (e.g., `/dev/ttyUSB0`).



## Running micro-ROS Agent (WiFi Communication)

To run the micro-ROS Agent over UDP (WiFi):

1. Upload the WiFi example code from Arduino IDE.
2. Run this Docker command:
   ```bash
   docker run -it --rm -v /dev:/dev --privileged --net=host \
     microros/micro-ros-agent:humble udp4 --port 8888
   ```

> **Note:** Ensure the same port number (e.g., 8888) is mentioned in the Arduino sketch as in the agent command above.


If you have any queries, please feel free to contact us at helpdesk@e-yantra.org.
