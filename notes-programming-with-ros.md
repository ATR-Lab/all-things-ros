Programming Robots with ROS Notes

# Glossary:

- **Degrees of Freedom (DoF)**
   - Lorem ipsum
- **Joint Space**
   - Lorem ipsum
- **Workspace**
   - Lorem ipsum
- **Obstacles**
   - Fixed objects or structures located in the worksapace, that the manipulator must avoid
- **Motion Planning**
   - It is the field of study that addresses the issues of avoiding obstacles
- **Range of Motion**
   - In many cases, each joint has a limited range of motion. Obstructions such a wires, hoses, mechanical structures, and other constraints often prevent manipulator joints from being able to spin endlessly
- **Map Frame**
   - Coordinate frame that is fixed relative to the environment and never moves
- **Robot Frame**
   - Cooridnate frame that is attached to the robot and moves with it
- **Localization Algorithms**
   - These algorithms seek to describe the relationship between the map frame and the robot frame
- **Joint State Vector**
   - Lorem ipsum
- **Task Space aka Cartesian Space**
   - The real-world space - a Cartesian world, not joint space
- **Forward Kinematics**
   - Converts from joint space of a manipulator to task space position of its end effector. This is done by applying geometric transformations - kinematic transformations. The goemetry includes how long each link is, the angles between the axes of rotation, and the joint angles.
   - NOTE: the forward kinematics function is fast an unambiguous: you put in a joint state, you get out a position.
   - ROS provides many tools for this, notably the *tf* package
- **Waypoints**
   - A set of position along the trajectory from position A to position B

# Chapter 2: Preliminaries
- ROS systems consist of a number of indpendent *nodes* that comprise a *graph*


# Chapter 3: Topics
- Nodes most commonly communicate through *topics*
- A *topic* is a name for a stream of messages with a defined type
- Example: A laser range-finder data might be sent on topic *scan*, with a message type of *LaserScan*
- Example: A camera might send data on a topic called *image*, with a message of type *Image*
- ROS implements a *public/subscribe* communication mechanism
- ROS' middleware requires a centralized broker that processes the topics each desires to subscribe or publish
- All messages on the same topic must be of the same data type
- Latched topics allow all subscribers to automatically get *the last message sent* when they subscribe to the topic
- List of message types is available in the ROS [Wiki](http://wiki.ros.org/msg#Field_Types?distro=kinetic)
- Messsages Types are hard definitions written on '.msg' file


# Chapter 4: Services
- Services are another way to pass data between ROS nodes
- Services are just synchronous remote procedure calls
- They allow one node to call a function that executes in another node
- The inputs and outputs are defined similarly as new message types
- The server (which provides the service) specifies a callback to deal with the service request, and advertises the service
- The client (which class the service) then accesses this service through a local proxy
- Requires a Service Server


## When to use
- Services are handy for simple get/set interactions like querying status and managing configuration, they don't work well when you need to initiate a long-running task
- Service calls are well suited to things that you only need to do occasionally and that *take a bounded* amount of time to complete
- An example of this is a 'common computation' that you might want to distributed to other computers
- Other exdamples include 'discrete actions' that the robot might do, such as turning on a sensor or taking a high-resolution picture with a camera


# Chapter 5: Actions
- Actions are the best way to implement interfaces to time-extended, goal-oriented bahaviors like *goto_position*
- Actions are *asynchronous*, while services are synchronous
- Actions use a *goal* to initiate a behavior and sends a *results* when the behavior is complete
- Actions further use *feedback* to provide updates on the behavior's progress towards the goal and also allows for goals to be canceled
- Actions themselves are implemented using topics
- An action can be seen as a high-level protocol that specifies how a set of topics (goal, result, feedback, etc) should be used in combination
- Requires an 'Action Server'

## When to use
- Actions are suitable for long-running tasks


# On Manipulators

## Joints

- In classical robotics, there are two major types of manipulator joing: (1) revolute and (2) prismatic
- Revolute joints ratotate about an *axis of rotation*. Also known as rotary joints
- Prismatic joints move linearly along an axis of motions like a sliding door or telescoping car radio antenna

## On Links

- A *link* is a section of a robot arm connected by a *joint*
- For example, your upper arm is a link, as is your lower arm
- A series of connected links and joint is known as a *kinematic chain*
- Knowing the geometry of a kinematic chain is a fundamental requirement of controlling a robotic manipulator
- Usually one side of a kinematic chain is considered to be *grounded*, meaning that it is fixed with respect to some other coordinate frame, such as a factory floor or the torso of a robot
- An *open kinematic* chain is one in which the non-grounded side of the chain is free to move around the workspace
- The free-floatin side of a manipulator is usually fitted with some sort of an *end effector*, such as a welding iron, a paint gun, a grinding wheel, or a general-purpose gripper or suction cup

## Kinematics

- Forwards Kinematics tells us where the end effector is, relative to the rest of the robo
- Inverse Kinematics tells, given a desired point in the world, what the arm's joint angles should be
- We can relatively quickly derive the inverse kinmatics equations for simple the two-dimensional arms
- But, things quickly get nasty when we move up to arms with more joints
- Once an arm has more than 6 joints, there is no longer a unique inverse kinematics solution! Instead there can be a *set* or *manifold* solutions, all of which achieve the desired end-effector position

## ROS Tools
- *tf* package is your best friend
- *Motion planners* are also your friends during manipulation. You simple thell them where the manipulator is, where you want it to be, and provide a description of the robot and its environment. The motion planner then performs some impressive mathematics and responds with a *trajectory* of joint state that you can feed to the manipulator's joint controllers


