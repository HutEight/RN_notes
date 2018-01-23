<img src="https://www.baesystems.com/cs/BAE-Static/latest/img/logo_baesystems_en.png?v=2.19.5"/> <img src="https://www.royalnavy.mod.uk/rnAssets/img/logo.png" width="45" height="54.5" />

# RN da Vinci Notes
Version 20180122

### Content Table

01. [Gazebo Simulation Launch Files and Models](https://github.com/HutEight/RN_notes/blob/master/RN_davinci_notes.md#gazebo-simulation-launch-files-and-models)


### Gazebo Simulation Launch Files and Models

01. Main launch file: e.g.[sticky_davinci_gazebo.launch]()

This section only introduces the files, including some other .launch files, launched by this launchfile.

You can add these lines to reset the Gazebo environment, so that its default models folder can be remapped to the path where you store all your models to be loaded into Gazebo.
```
<env name="GAZEBO_MODEL_PATH" value="$(find cwru_davinci_gazebo)/model"/>
<env name="GAZEBO_MODEL_PATH" value="$(find cwru_davinci_gazebo)/props"/>
```

It should first launch a **.world file**
```
<include file="$(find cwru_davinci_gazebo)/launch/empty_world.launch">
  <arg name="world_name" value="$(find cwru_davinci_gazebo)/world/sticky_davinci.world"/>
	<arg name="debug" value="$(arg debug)" />
	<arg name="gui" value="$(arg gui)" />
	<arg name="paused" value="$(arg paused)"/>
	<arg name="use_sim_time" value="$(arg use_sim_time)"/>
	<arg name="headless" value="$(arg headless)"/>
</include>
```

It then load the robot description **.xacro**, and spwan a rbot into Gazebo.
```
<param name="robot_description" command="$(find xacro)/xacro.py '$(find cwru_davinci_gazebo)/model/both_psms_sticky.urdf.xacro'" />
<!-- Spawn a robot into Gazebo -->
<node name="spawn_urdf" pkg="gazebo_ros" type="spawn_model" args="-param robot_description -urdf -model davinci">
</node>
```

Next, the ros_control **.launch** file.
```
<include file="$(find cwru_davinci_gazebo)/launch/davinci_control_both.launch">
</include>
```

02. Gazebo world file: e.g.[sticky_davinci.world]()

It loads the ground, the sun, and other objects you might want to add to your scene.

03. Robot description Xacro file: e.g.[both_psms_sticky.urdf.xacro]()

It describes the links,the joints, and the Gazebo plugins that you use for the robot or camera control. This file essentially defines the all the transforms of the robot.

04. Ros controller launch file: e.g.[davinci_control_both.launch]()







