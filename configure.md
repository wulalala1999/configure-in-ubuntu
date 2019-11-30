### Hades Canyon Configuration

Copyright © 2018 FortiSTray_Action. All Rights Reserved.

---
#### How to install ubuntu alongside Windows
##### Refer to this article to assign disks
https://blog.csdn.net/flyyufenfei/article/details/79187656


#### Preparation before installing libraries

##### Change Ubuntu source to tuna

```bash
sudo gedit /etc/apt/sources.list
```

Replace all contains to follows

```bash
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-proposed main restricted universe multiverse
```

```bash
sudo apt-get update && sudo apt-get upgrade 
```

##### Install Git

```bash
sudo apt-get install git
```

##### Install CMake

```bash
sudo apt-get install cmake
```

#### Install librealsense (v2.16.1)

* Download source code from Github (Release > Intel® RealSense™ SDK 2.0 (build 2.16.1))

  Extract the `.tar.gz` file to `~/Library`

  Unplug any connected Intel RealSense camera

* Navigate to librealsense root directory

  ```bash
  sudo apt-get install libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev
  sudo apt-get install libglfw3-dev
  sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/ 
  sudo udevadm control --reload-rules && udevadm trigger
  ./scripts/patch-realsense-ubuntu-lts.sh
  echo 'hid_sensor_custom' | sudo tee -a /etc/modules
  mkdir build && cd build
  cmake .. -DCMAKE_BUILD_TYPE=Release
  sudo make uninstall && make clean && make -j8 && sudo make install
  ```

#### Install PCL (v1.8.1)

* Download source code from Github (Release > pcl-1.8.1)

  Extract the `.tar.gz` file to `~/Library`

* Navigate to PCL root directory

  ```bash
  sudo apt install libboost-all-dev libeigen3-dev libflann-dev libvtk6-dev
  sudo apt install libproj-dev
  mkdir build && cd build
  cmake -DCMAKE_BUILD_TYPE=Release ..
  make -j8
  sudo make -j8 install
  ```

#### Install OpenCV (v3.4.4) with OpenCV_Contrib (v3.4.4)

- Download OpenCV source code from Github (Release > OpenCV 3.4.4)

  Download OpenCV_Contrib source code from Github (Release > 3.4.4)

  Extract the `.tar.gz` file to `~/Library`

  Copy OpenCV_Contrib folder into OpenCV folder and rename it as `opencv_contrib`

- Navigate to OpenCV root directory

  ```bash
  sudo apt-get install build-essential
  sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
  mkdir build && cd build
  cmake -DCMAKE_BUILD_TYPE=Release ..
  make -j8
  sudo make install
  ```

#### Work environment optimization

##### Install chromium

```bash
sudo apt-get install chromium-browser
```

##### Install Sogou Pinyin input method

Download `.deb` file from official website

```bash
sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb
sudo apt-get install -f
```

Set `System Settings > Language Support > Keyboard input method system = fcitx`

Log out &  Log in

Keyboard icon on the right top > add `Sogou Pinyin`

```bash
sudo apt-get remove fcitx-ui-qimpanel
```

Log out &  Log in

##### Install vscode

Download `.deb` file from official website

```bash
sudo apt-get install -f
sudo dpkg -i code_1.29.1-1542309157_amd64.deb
```
##### Resolve dependencies
```bash
sudo apt-get install -f
```



