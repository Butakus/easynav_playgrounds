<!--
Copyright 2026 Intelligent Robotics Lab
SPDX-License-Identifier: Apache-2.0
-->

# EasyNav PlayGrounds — `pichi-workshop` branch

This branch is a trimmed copy of the [`lyrical`](https://github.com/EasyNavigation/easynav_playgrounds/tree/lyrical) branch for the workshop *Desde que uso Pixi estoy tan Pichi* (reproducible ROS 2 workspaces with Pixi and RoboStack).
It only keeps the Kobuki simulation, without EasyNav, so that participants can build a third-party workspace in a few seconds:

| Package | Contents |
| --- | --- |
| [`easynav_playground_kobuki_description`](playground_kobuki/easynav_playground_kobuki_description) | The Kobuki (Turtlebot 2) model: URDF and meshes |
| [`easynav_playground_kobuki_worlds`](playground_kobuki/easynav_playground_kobuki_worlds) | The Gazebo simulation: AWS small house world, its map, and the launchers that spawn the Kobuki with the ROS–Gazebo bridge |

For the full playgrounds (Kobuki, Summit XL, TIAGo, omnidirectional robots) and their EasyNav configurations, use the distribution branches (`jazzy`, `kilted`, `lyrical`, `rolling`).

## Build and run with Pixi

From the root of a ROS 2 workspace with this repository in `src/`:

```bash
pixi init -c https://prefix.dev/robostack-lyrical -c conda-forge
pixi add ros-lyrical-ros-base ros-dev-tools ros-lyrical-ros-gz-sim ros-lyrical-ros-gz-bridge \
  ros-lyrical-gz-sim-vendor ros-lyrical-xacro ros-lyrical-robot-state-publisher ros-lyrical-launch-yaml
pixi run colcon build
pixi shell
source install/setup.bash
ros2 launch easynav_playground_kobuki_worlds gazebo_sim.launch.yaml
```

Drive the robot from another terminal, for example with `teleop_twist_keyboard` (it publishes `geometry_msgs/msg/Twist` on `/cmd_vel`).

Each package also has a `pixi.toml` for the `pixi-build-ros` backend, so it can be built and published as a conda package with `pixi publish`.

## Licensing

Each package declares its licenses in its `package.xml` and explains them in its README: Yujin Robot's Kobuki model (BSD-3-Clause), AWS RoboMaker's small house (MIT-0), and the launchers and configuration by the [Intelligent Robotics Lab](https://intelligentroboticslab.gsyc.urjc.es/) (Apache-2.0).
