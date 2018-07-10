# ROS Cheatsheet

# Workspace

```
# Make sure you've added the system-wide ROS setup script to .bashrc file
# If you haven't done that, do it now, or source the file by hand

souce /opt/ros/kinetic/setup.bash
```

```
# Create a new workspace

# STEP 1: Create a new workspace folder, e.g. telebot_ws
mkdir -p /telebot_ws/src
cd telebot_ws/src
catkin_init_workspace

# STEP 2: Create the catkin workspace files
cd ../telebot_ws
catking_make
```

# Packages

```
# Go into the workspace src directory
cd telebot_ws/src
```

```
# Create package e.g. my_awesome_code
catkin_create_pkg my_awesome_code rospy
```

# Topics

```
# List all topics
rostopic list
```

```
# Show the messages being to a given topic
rostopic echo

# Example for a node called 'counter'. Show only 5 messages
rostopic echo counter -n 5
```

```
# Verify that we are publishing at the correct rate
rostopic hz conunter
```

```
# Find more information about an advertised topic
rostopic info

# Example for a node called 'counter'
rostopic info counter
```

```
# Find topics that publish a given message type
rostopic find

# Example for a topic with 'std_msgs/Int32' type
rostopic find std_msgs/Int32
```

```
# Publish a message to a topic
rostopic pub [topic_name] [message_type] [message_data]

# Example
rostopic pub counter std_msgs/Int32 1000000
```

```
# Help on rostopic parameters
rostopic -h
```

