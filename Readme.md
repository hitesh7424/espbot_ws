# ESPBot ROS 2 Workspace

A ROS 2 (Jazzy) workspace containing Python and C++ examples for publishers and subscribers.

---

## Table of Contents

- [Dependencies](#dependencies)
- [Workspace Setup](#workspace-setup)
- [Package Structure](#package-structure)
- [Examples](#examples)
  - [Simple Publisher (Python)](#simple-publisher-python)
  - [Simple Publisher (C++)](#simple-publisher-c)
  - [Simple Subscriber (Python)](#simple-subscriber-python)
  - [Simple Subscriber (C++)](#simple-subscriber-c)
- [Useful ROS 2 Topic Commands](#useful-ros-2-topic-commands)

---

## Dependencies

Install the required ROS 2 packages and Python libraries:

```bash
sudo apt install ros-jazzy-joint-state-publisher-gui
sudo apt install ros-jazzy-xacro
sudo apt install ros-jazzy-ros-gz*
sudo apt install ros-jazzy-ros2-control
sudo apt install ros-jazzy-ros2-controllers
sudo apt install ros-jazzy-gz-ros2-control*
sudo apt install ros-jazzy-moveit*
sudo apt install libserial-dev
sudo apt install python3-pip

pip install pyserial --break-system-packages
pip install flask --break-system-packages
pip install flask-ask-sdk --break-system-packages
pip install ask-sdk --break-system-packages
```


---

## Workspace Setup

```bash
mkdir -p ~/espbot_ws/src
cd ~/espbot_ws
colcon build
source install/setup.bash
```

---

## Package Structure

Two packages are created inside `src/`:

| Package | Build Type | Language |
|---|---|---|
| `espbot_py_examples` | `ament_python` | Python |
| `espbot_cpp_examples` | `ament_cmake` | C++ |

### Create the packages

```bash
cd ~/espbot_ws/src

ros2 pkg create --build-type ament_python espbot_py_examples
ros2 pkg create --build-type ament_cmake espbot_cpp_examples
```

### Build and source

```bash
cd ~/espbot_ws
colcon build
source install/setup.bash
```

### Verify packages are found

```bash
ros2 pkg list | grep esp
# espbot_cpp_examples
# espbot_py_examples
```

---

## Examples




### Simple Publisher (Python)

Publishes a `std_msgs/msg/String` message to the `/chatter` topic at **1 Hz**.

**Run:**
```bash
colcon build && source install/setup.bash
ros2 run espbot_py_examples simple_publisher
```

**Output:**
```
[INFO] [simple_publisher]: Publishing at 1.0 Hz
```

**Topic:** `/chatter` | **Type:** `std_msgs/msg/String` | **Rate:** 1 Hz

---









### Simple Publisher (C++)

Publishes a `std_msgs/msg/String` message to the `/chatter` topic at **1 Hz**.

**Run:**
```bash
colcon build && source install/setup.bash
ros2 run espbot_cpp_examples simple_publisher
```

**Output:**
```
[INFO] [simple_publisher]: Publishing at 1 Hz
```

**Topic:** `/chatter` | **Type:** `std_msgs/msg/String` | **Rate:** 1 Hz

---




### Simple Subscriber (Python)

Subscribes to the `/chatter` topic and prints each received message.

**Run:**
```bash
colcon build && source install/setup.bash
ros2 run espbot_py_examples simple_subscriber
```

**Output:**
```
[INFO] [simple_subscriber]: I heard: Hello ROS 2 - counter: 0
[INFO] [simple_subscriber]: I heard: Hello ROS 2 - counter: 1
```

**Topic:** `/chatter` | **Type:** `std_msgs/msg/String`

---



### Simple Subscriber (C++)

Subscribes to the `/chatter` topic and prints each received message.

**Run:**
```bash
colcon build && source install/setup.bash
ros2 run espbot_cpp_examples simple_subscriber
```

**Output:**
```
[INFO] [simple_subscriber]: I heard: Hello ROS 2 - Counter: 0
[INFO] [simple_subscriber]: I heard: Hello ROS 2 - Counter: 1
```

**Topic:** `/chatter` | **Type:** `std_msgs/msg/String`

---

## Useful ROS 2 Topic Commands

```bash
# List all active topics
ros2 topic list

# Print messages being published on a topic
ros2 topic echo /chatter

# Show publisher/subscriber count and message type
ros2 topic info /chatter

# Show detailed info including QoS profile
ros2 topic info /chatter --verbose

# Check publishing frequency
ros2 topic hz /chatter

# Publish a single message manually
ros2 topic pub /chatter std_msgs/msg/String '{"data": "hello"}' --once

# Publish continuously
ros2 topic pub /chatter std_msgs/msg/String '{"data": "hello"}'
```

