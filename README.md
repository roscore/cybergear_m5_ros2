# cybergear_m5_ros2

ROS2 package for Xiaomi Cybergear.

> [!WARNING]  
> Xiaomi Cybergear can generate high torque, so please make control parameter adjustments at your own risk.

## Dev Environments

* Host OS
  * ubuntu 20.04

* Applciations
  * Docker       : docker-ce 24.0.6
  * Container OS : Ubuntu 22.04
  * Middleware   : ROS2 (humble)

## How to build dev-environments

Create dev-environment on docker using follow commands.
`docker compose up` command launch terminator (blue color) that develop with ros2 humble.
This docker container contains ros2-humble and necessary software to launch samples.

```bash
cd docker

# please check and modify follow env vairables at this script.
# WORKSPACE_DIR ... mount diretory
# SERIAL_DEVICE ... serial device name
bash generate_env.bash

# build docker container
docker-compose build

# launch container
docker compose up
```

## Build from source

```bash
source /opt/ros/humble/setup.bash

# make ros2 workspace
export COLCON_WS=~/ws
mkdir -p $COLCON_WS/src

# clone cybergear_m5 source
cd $COLCON_WS/src
git clone git@github.com:project-sternbergia/cybergear_m5_ros2.git
cd ../

# build ros2 package
colcon build
```

## Prepare M5 stack

Before launch sample, please write `cybergear_m5_bridge.ino` to m5 stack.
Please refer [cyberger_m5](https://github.com/project-sternbergia/cybergear_m5) repository.

## How to run sample bridge node

### rviz2 samples (joint_state_publisher_gui samples)

Please test simple sample code.

```bash
cd $COLCON_WS
source install/setup.bash

# 1dof cybergear position control sample
# you control cybergear via joint_state_publisher_gui
# cybergear can id : 0x7F
ros2 launch cybergear_m5_bringup 1dof_position_sample.launch.xml

# 2dof cybergear position control sample
# you control cybergear via joint_state_publisher_gui
# cybergear_1 can id : 0x7F
# cybergear_2 can id : 0x7E
ros2 launch cybergear_m5_bringup 2dof_position_sample.launch.xml
```

If you want to change control parameter, please check config file at `cybergear_m5_description/config` directory.

`2dof_position_sample.launch.xml`

![cybergear_ros2_bridge_example](docs/img/cybergear_ros2_bridge_sample.gif)

## LICENSE

* MIT

## References

##이슈 잇슈

```
[INFO] [launch]: All log files can be found below /home/pjs/.ros/log/2023-12-05-22-48-30-553965-pjs-20720
[INFO] [launch]: Default logging verbosity is set to INFO
Task exception was never retrieved
future: <Task finished name='Task-2' coro=<LaunchService._process_one_event() done, defined at /opt/ros/foxy/lib/python3.8/site-packages/launch/launch_service.py:226> exception=PackageNotFoundError("package 'joint_state_publisher_gui' not found, searching: ['/home/pjs/capstone_ws/install/robot_arm_mujoco', '/home/pjs/capstone_ws/install/robot_arm_manager', '/home/pjs/capstone_ws/install/robot_arm_kinematicdynamic', '/home/pjs/capstone_ws/install/position_msgs', '/home/pjs/capstone_ws/install/cybergear_m5', '/home/pjs/capstone_ws/install/cybergear_m5_bringup', '/home/pjs/capstone_ws/install/cybergear_m5_driver', '/home/pjs/capstone_ws/install/cybergear_description', '/opt/ros/foxy']")>
Traceback (most recent call last):
  File "/opt/ros/foxy/lib/python3.8/site-packages/ament_index_python/packages.py", line 50, in get_package_prefix
    content, package_prefix = get_resource('packages', package_name)
  File "/opt/ros/foxy/lib/python3.8/site-packages/ament_index_python/resources.py", line 48, in get_resource
    raise LookupError(
LookupError: Could not find the resource 'joint_state_publisher_gui' of type 'packages'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/launch_service.py", line 228, in _process_one_event
    await self.__process_event(next_event)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/launch_service.py", line 248, in __process_event
    visit_all_entities_and_collect_futures(entity, self.__context))
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/utilities/visit_all_entities_and_collect_futures_impl.py", line 45, in visit_all_entities_and_collect_futures
    futures_to_return += visit_all_entities_and_collect_futures(sub_entity, context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/utilities/visit_all_entities_and_collect_futures_impl.py", line 45, in visit_all_entities_and_collect_futures
    futures_to_return += visit_all_entities_and_collect_futures(sub_entity, context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/utilities/visit_all_entities_and_collect_futures_impl.py", line 45, in visit_all_entities_and_collect_futures
    futures_to_return += visit_all_entities_and_collect_futures(sub_entity, context)
  [Previous line repeated 4 more times]
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/utilities/visit_all_entities_and_collect_futures_impl.py", line 38, in visit_all_entities_and_collect_futures
    sub_entities = entity.visit(context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/action.py", line 108, in visit
    return self.execute(context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch_ros/actions/node.py", line 453, in execute
    ret = super().execute(context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/actions/execute_process.py", line 823, in execute
    self.__expand_substitutions(context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/actions/execute_process.py", line 668, in __expand_substitutions
    cmd = [perform_substitutions(context, x) for x in self.__cmd]
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/actions/execute_process.py", line 668, in <listcomp>
    cmd = [perform_substitutions(context, x) for x in self.__cmd]
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/utilities/perform_substitutions_impl.py", line 26, in perform_substitutions
    return ''.join([context.perform_substitution(sub) for sub in subs])
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/utilities/perform_substitutions_impl.py", line 26, in <listcomp>
    return ''.join([context.perform_substitution(sub) for sub in subs])
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/launch_context.py", line 232, in perform_substitution
    return substitution.perform(self)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch_ros/substitutions/executable_in_package.py", line 76, in perform
    package_prefix = super().perform(context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch_ros/substitutions/find_package.py", line 79, in perform
    result = self.find(package)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch_ros/substitutions/find_package.py", line 96, in find
    return get_package_prefix(package_name)
  File "/opt/ros/foxy/lib/python3.8/site-packages/ament_index_python/packages.py", line 52, in get_package_prefix
    raise PackageNotFoundError(
ament_index_python.packages.PackageNotFoundError: "package 'joint_state_publisher_gui' not found, searching: ['/home/pjs/capstone_ws/install/robot_arm_mujoco', '/home/pjs/capstone_ws/install/robot_arm_manager', '/home/pjs/capstone_ws/install/robot_arm_kinematicdynamic', '/home/pjs/capstone_ws/install/position_msgs', '/home/pjs/capstone_ws/install/cybergear_m5', '/home/pjs/capstone_ws/install/cybergear_m5_bringup', '/home/pjs/capstone_ws/install/cybergear_m5_driver', '/home/pjs/capstone_ws/install/cybergear_description', '/opt/ros/foxy']"
Task exception was never retrieved
future: <Task finished name='Task-16' coro=<LaunchService._process_one_event() done, defined at /opt/ros/foxy/lib/python3.8/site-packages/launch/launch_service.py:226> exception=RuntimeError('Signal event received before subprocess transport available.')>
Traceback (most recent call last):
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/launch_service.py", line 228, in _process_one_event
    await self.__process_event(next_event)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/launch_service.py", line 248, in __process_event
    visit_all_entities_and_collect_futures(entity, self.__context))
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/utilities/visit_all_entities_and_collect_futures_impl.py", line 38, in visit_all_entities_and_collect_futures
    sub_entities = entity.visit(context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/action.py", line 108, in visit
    return self.execute(context)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/actions/opaque_function.py", line 75, in execute
    return self.__function(context, *self.__args, **self.__kwargs)
  File "/opt/ros/foxy/lib/python3.8/site-packages/launch/actions/execute_process.py", line 443, in __on_signal_process_event
    raise RuntimeError('Signal event received before subprocess transport available.')
RuntimeError: Signal event received before subprocess transport available.
[INFO] [cybergear_m5_bridge_node-1]: process started with pid [20724]
[INFO] [robot_state_publisher-2]: process started with pid [20726]
[INFO] [rviz2-3]: process started with pid [20728]
[INFO] [robot_state_publisher-2]: sending signal 'SIGINT' to process[robot_state_publisher-2]
[INFO] [cybergear_m5_bridge_node-1]: sending signal 'SIGINT' to process[cybergear_m5_bridge_node-1]
[ERROR] [robot_state_publisher-2]: process has died [pid 20726, exit code -2, cmd '/opt/ros/foxy/lib/robot_state_publisher/robot_state_publisher --ros-args --params-file /tmp/launch_params_tk95kk4p'].
[ERROR] [cybergear_m5_bridge_node-1]: process has died [pid 20724, exit code -2, cmd '/home/pjs/capstone_ws/install/cybergear_m5_driver/lib/cybergear_m5_driver/cybergear_m5_bridge_node --ros-args --params-file /tmp/launch_params_v8ym89ev --params-file /tmp/launch_params_vweps7q3 --params-file /tmp/launch_params_qkybwel9 --params-file /tmp/launch_params_6vv234g5 --params-file /tmp/launch_params_vwv019rr --params-file /tmp/launch_params_ucd9dwih --params-file /home/pjs/capstone_ws/install/cybergear_m5_bringup/share/cybergear_m5_bringup/config/1dof_position_sample.yaml'].
[rviz2-3] [INFO]: Stereo is NOT SUPPORTED
[rviz2-3] [INFO]: OpenGl version: 4.6 (GLSL 4.6)
[rviz2-3] [INFO]: Stereo is NOT SUPPORTED
[rviz2-3] [ERROR]: PluginlibFactory: The plugin for class 'rviz_common/Time' failed to load. Error: According to the loaded plugin descriptions the class rviz_common/Time with base class type rviz_common::Panel does not exist. Declared types are 
[ERROR] [rviz2-3]: process[rviz2-3] failed to terminate '5' seconds after receiving 'SIGINT', escalating to 'SIGTERM'
[INFO] [rviz2-3]: sending signal 'SIGTERM' to process[rviz2-3]
[ERROR] [rviz2-3]: process has died [pid 20728, exit code -15, cmd '/opt/ros/foxy/lib/rviz2/rviz2 -d /home/pjs/capstone_ws/install/cybergear_description/share/cybergear_description/rviz/rviz.rviz --ros-args --params-file /tmp/launch_params_udcjuhx3'].

```

* [cybergear_m5](https://github.com/project-sternbergia/cybergear_m5)
