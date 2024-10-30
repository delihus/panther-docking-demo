# panther-docking-demo

## Usage

### Clone panther_ros workspace

```bash
mkdir -p husarion_ws/src
git clone https://github.com/husarion/panther_ros.git -b ros2-docking husarion_ws/src
vcs import husarion_ws/src < husarion_ws/src/panther/panther_hardware.repos
```

### Sync workspace with user computer

```bash
./sync_with_user_computer.sh
```

### Log into the user computer

```bash
ssh husarion@10.15.20.3
```

### Build `panther_docking` on the user computer

```bash
cd panther-docking-demo/husarion_ws
colcon build --symlink-install --packages-up-to panther_docking --cmake-args -DCMAKE_BUILD_TYPE=Release
```

### Run Docking Demo

Inside  `panther-docking-demo/husarion_ws` run:

```bash
source install/setup.bash
ros2 launch panther_docking docking.launch.py namespace:=panther apriltag_id:=0
```

In a new terminal on the user computer run:

```bash
cd panther-docking-demo
docker compose up
```

### Dock action

```bash
ros2 action send_goal /panther/dock_robot opennav_docking_msgs/action/DockRobot " {  dock_type: panther_charging_dock, navigate_to_staging_pose: false, dock_id: main_dock }"
```

### Undock action

```bash
ros2 action send_goal /panther/undock_robot opennav_docking_msgs/action/UndockRobot " {  dock_type: panther_charging_dock }"
```
