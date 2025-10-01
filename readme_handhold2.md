# FAST-LIVO2-Humble-handhold2
This repository demonstrates how to run **[handhold2](https://github.com/hku-mars/LIV_handhold_2)** on **fast-livo2 (Humble)**.

### Complete Reproduction Process:
1. Purchase the required items  
2. 3D Printing: (LiDAR parts do not require supports, while the camera parts require supports)  
3. Testing: First, verify that both the LiDAR and camera can successfully publish messages  
4. Calibration: Camera intrinsics → Camera–LiDAR extrinsics ([manual calibration here](https://github.com/Longxiaoze/mvs_ros_driver2/tree/main/scripts))  
5. Fill the calibration results into the parameter files of fast-livo2  
6. Follow the installation and execution steps below to run

## install 

### fast-livo2 and Hikvision driver
**[fastlivo2 humble](https://github.com/Longxiaoze/FAST-LIVO2/tree/handhold2)** + **[Hikvision MV-CU013-A0UC driver](https://github.com/Longxiaoze/mvs_ros_driver2)**

Please install [MVS SDK](https://www.hikrobotics.com/en/machinevision/service/download/) firstly!!! (tested on mvs 4.6.0)

``` bash
mkdir -p  ~/fast_livo2_handhold2_ws/src
cd ~/fast_livo2_handhold2_ws/src
git clone -b handhold2 https://github.com/Longxiaoze/FAST-LIVO2.git
git clone -b handhold2 https://github.com/Longxiaoze/livox_ros2_driver.git
git clone https://github.com/Longxiaoze/rpg_vikit.git
git clone https://github.com/Longxiaoze/sophus.git
# you need to install MVS SDK firstly.
git clone https://github.com/Longxiaoze/mvs_ros_driver2

cd ~/fast_livo2_handhold2_ws
colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
```

### Livox Mid-360 driver
**[mid-360 driver](https://github.com/Longxiaoze/livox_ros_driver2)** 
``` bash
mkdir -p ~/fast_livo2_handhold2_livox_ws/src
cd ~/fast_livo2_handhold2_livox_ws/src
git clone https://github.com/Longxiaoze/livox_ros_driver2.git
cd livox_ros_driver2
bash ./build.sh humble
```


## run
### Hikvision camera
``` bash
export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
source ~/fast_livo2_handhold2_ws/install/setup.bash
ros2 launch mvs_ros2_driver single_camera.py
```

### Mid-360 driver
``` bash
source ~/fast_livo2_handhold2_livox_ws/install/setup.bash
ros2 launch livox_ros_driver2 msg_MID360_launch.py
```

### fastlivo2 humble
``` bash
export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
source ~/fast_livo2_handhold2_ws/install/setup.bash
ros2 launch fast_livo mapping_avia.launch.py
```
