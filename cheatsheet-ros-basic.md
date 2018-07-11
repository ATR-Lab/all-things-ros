# ROS Cheatsheet

## Workspace

### Sourcing ROS
```
# Make sure you've added the system-wide ROS setup script to .bashrc file
# If you haven't done that, do it now, or source the file by hand

souce /opt/ros/kinetic/setup.bash
```

### Creating a new workspace

#### STEP 1: Create a new workspace folder
```
# Create a new workspace folder, e.g. telebot_ws
mkdir -p /telebot_ws/src
```
#### STEP 2: Initialize the workspace
```
# Enter the src directory
cd telebot_ws/src

# Use catkin to initialize workspace
catkin_init_workspace
```

#### STEP 3: Generate the catkin workspace files
```
# Generate the catkin workspace files
cd ../telebot_ws
catkin_make
```

## Packages

```
# Go into the workspace src directory
cd telebot_ws/src
```

```
# Create package e.g. my_awesome_code
catkin_create_pkg my_awesome_code rospy
```

## Topics

### Help on rostopic parameters
```
rostopic -h
```

### List all topics
```
rostopic list
```
### Show messages published to a topic
```
rostopic echo [topic-name] [param] [param-value]

# For example, for a node called 'counter'. Show only 5 messages
rostopic echo counter -n 5
```

### Check publish rate
```
rostopic hz [topic-name]

# For example, for a node named 'counter'
rostopic hz counter
```

### Display information about an advertised topic
```
rostopic info [topic-name]

# For example, for a node called 'counter'
rostopic info counter
```

### Find topics of a given message type
```
rostopic find [message-type]

# For example, for a topic with 'std_msgs/Int32' type
rostopic find std_msgs/Int32
```

### Publis a message to a topic
```
rostopic pub [topic_name] [message_type] [message_data]

# For example, for a topic named 'counter', publish a message with a type of 'std_msg/Int32' and a value 1000000
rostopic pub counter std_msgs/Int32 1000000
```
