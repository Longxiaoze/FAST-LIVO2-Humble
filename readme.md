# ROS2 Version FAST-LIVO2
This library is used to demonstrate how to install and run the Humble version of fast-livo2.

tested on ubuntu22 ros2 humble

## install
``` bash
mkdir -p ~/fast_livo2_ws/src
cd ~/fast_livo2_ws/src

git clone https://github.com/Longxiaoze/FAST-LIVO2.git
git clone https://github.com/Longxiaoze/livox_ros2_driver.git
git clone https://github.com/Longxiaoze/rpg_vikit.git
git clone https://github.com/Longxiaoze/sophus.git

cd ~/fast_livo2_ws
colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
```

## run fast-livo2
``` bash
source ~/fast_livo2_ws/install/setup.bash
ros2 launch fast_livo mapping_avia.launch.py
```


## play ros2 bag file
Please change config file first (I changed them for my datasets)
### ROS1 bagfile --> ROS2 bagfile(humble)
``` bash
sudo apt install ros-humble-rosbag2 ros-humble-rosbags-convert
rosbags-convert --src CBD_Building_01.bag --dst CBD_Building_01
```

and change following:

``` diff
    topic_metadata:
      name: /livox/lidar
      offered_qos_profiles: ''
      serialization_format: cdr
-     type: livox_ros_driver/msg/CustomMsg
+     type: livox_interfaces/msg/CustomMsg

      type_description_hash: RIHS01_94041b4794f52c1d81def2989107fc898a62dacb7a39d5dbe80d4b55e538bf6d
```

### play ros2 bag file
``` bash
source ~/fast_livo2_ws/install/setup.bash
ros2 bag play /path/to/CBD_Building_01
```

## Thanks
Thank you for their great work：

[hku-mars/FAST-LIVO2]()

[shamanqing1/fast_livo2_ros2](https://github.com/shamanqing1/fast_livo2_ros2)

[ROS2 HUMBLE Migration #128](https://github.com/hku-mars/FAST-LIVO2/issues/128)
