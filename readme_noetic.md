# Fast-livo2 ros noetic on Unitree robot
Tested on Go2 R&D jetson nx

## Sophus
``` bash
mkdir ~/packages
cd ~/packages
git clone https://github.com/strasdat/Sophus.git
cd Sophus
git checkout a621ff
mkdir build && cd build && cmake ..
make
sudo make install
```

``` c++
// sophus/so2.cpp
unit_complex_.real() = 1.;
unit_complex_.imag() = 0.;
//替换为对 complex 整体赋值（兼容性最好）：
unit_complex_ = std::complex<double>(1.0, 0.0);
```

## Livox SDK
Please install Livox SDK2 follow the guidance of installation in the [Livox-SDK2/README.md](https://github.com/Livox-SDK/Livox-SDK2/blob/master/README.md)
``` bash
mkdir ~/packages
cd ~/packages
git clone https://github.com/Livox-SDK/Livox-SDK2.git
cd ./Livox-SDK2/
mkdir build
cd build
cmake .. && make -j
sudo make install
```

## Livox
``` bash
mkdir ~/packages
cd ~/packages
git clone https://github.com/hku-mars/LIV_handhold_2
mkdir -p ~/fast_livo2_handhold2_livox_ws/src
cd ~/fast_livo2_handhold2_livox_ws/src
mv ~/packages/LIV_handhold_2/livox_ros_driver2 ./
cd livox_ros_driver2
bash ./build.sh ROS1
```


## MVS
Please install [MVS SDK](https://www.hikrobotics.com/en/machinevision/service/download/) first!!! (Tested MVS 3.0.1 aarch64 on jetpack5.1 ubuntu20 noetic)
``` bash
mkdir -p  ~/fast_livo2_handhold2_ws/src
cd ~/fast_livo2_handhold2_ws/src
git clone -b ros1 https://github.com/Longxiaoze/mvs_ros_driver2
```

## Fast-livo2 noetic
``` bash
cd ~/fast_livo2_handhold2_ws/src
git clone https://github.com/hku-mars/FAST-LIVO2
git clone https://github.com/xuankuzcr/rpg_vikit.git 
cd ~/fast_livo2_handhold2_ws
catkin_make -DCMAKE_EXE_LINKER_FLAGS="-lusb-1.0"
source ~/fast_livo2_handhold2_ws/devel/setup.bash
```

# run
``` bash
source ~/fast_livo2_handhold2_ws/devel/setup.bash
roslaunch mvs_ros2_driver single_camera.launch
```

``` bash
source ~/fast_livo2_handhold2_livox_ws/devel/setup.bash
# roslaunch livox_ros_driver2 rviz_MID360.launch 
roslaunch livox_ros_driver2 msg_MID360.launch
```

``` bash
source ~/fast_livo2_handhold2_ws/devel/setup.bash
export LD_LIBRARY_PATH=/lib/aarch64-linux-gnu:/usr/lib/aarch64-linux-gnu:$LD_LIBRARY_PATH
roslaunch fast_livo mapping_avia.launch
```
