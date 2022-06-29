# The Ros Fedora Project
# Installing Build Dependencies/Tools 
Run to install the compiler tools: 
```
sudo dnf install gcc-c++ python3-rosdep @buildsys-build
```
To compile ros you will use catkin_tool
To install catkin_tools run
```
sudo pip3 install -U catkin_tools
```
# Ros
# Initialize rosdep
```
sudo rosdep init
rosdep update
```

In order to build the core packages, you will need a catkin workspace. Create one now:
```
mkdir ~/ros_catkin_ws
cd ~/ros_catkin_ws
```

Download the source file with a git or directly as you want it's not my business.
Put your src in the catkin workspace.

```
git clone https://github.com/Tiqo01/Ros-Fedora.git
```

# Resolving Dependencies

Before building your catkin workspace you need to make sure that you have all the system dependencies on your platform. We use the rosdep tool for this:
```diff
-You can ignore the errors related to gazebo_dev

rosdep install --from-paths ./src --ignore-packages-from-source --rosdistro noetic -y -r
```


It is also necessary to install ogre, gazebo and ignition

```
sudo dnf install ogre-* gazebo-* ignition-*
```
# Workspace configuration

Run

```
cd ~/ros_catkin_ws
catkin init
catkin --config install
catkin build -DCMAKE_BUILD_TYPE=Release -DCATKIN_ENABLE_TESTING=0
echo "source ~/ros_catkin_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

If you have this error
```
EXCEPTION: Unable to create the rendering window
```
This is a known bug caused by Wayland, you have to configure Xorg as the default GNOME session,
[Configuring Xorg as the default GNOME session](https://docs.fedoraproject.org/en-US/quick-docs/configuring-xorg-as-default-gnome-session/)

1. Uncomment the line on the  /etc/gdm/custom.conf:
```
WaylandEnable=false
```
2. Add the following line to the [daemon] section:
```
DefaultSession=gnome-xorg.desktop
```
3. Save the custom.conf file.

4. Logout or reboot to enter the new session.

Enjoy.

