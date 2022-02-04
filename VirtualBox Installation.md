# Ubuntu 20.04 installation in VirtualBox


## VirtualBox for Windows

1. Go to the VirtualBox website https://www.virtualbox.org/wiki/Downloads
2. Select Windows distributions:

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204081944326.png" />


​	The following file will be downloaded:

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204082054360.png" />

3. Double click the executable file and complete installation:


<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204082237564.png" />



Once installation is completed VirtualBox you should see the following window:

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204082726789.png" />



## Download Ubuntu 20.04 distribution

1. Go to the Ubuntu website: https://ubuntu.com/download/desktop and click the **Download** button.

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204083229440.png"/>

The following file will be downloaded:

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204083332906.png" />



## Installing Ubuntu 20.04 in VirtualBox

1. Open VirtualBox app, and click **New** button:

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204083621185.png" />



2. Create Virtual machine, 

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204083835469.png" />

3. Select **Memory Size** in your system (8 GB recommended)

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204084007465.png" />

4. Select `Create a virtual hard disk now`, use default recommended. Recommended space 30 GB. This step may take a couple minutes

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204084306083.png" />

   When completed the following screen should appear:

   

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204084408179.png" alt="image-20220204084408179" style="zoom:67%;" />

Click **Start** button to start virtual machine

5. Select the downloaded `.iso` file then proceed with Ubuntu 20.04 installation



## Installation of Dependencies



1. Open a terminal (CTRL+ALT+T)

   ```bash
   $ sudo apt-get update
   $ sudo apt-get upgrade
   ```

   

2. Test screen

   ```bash
   $ xcalc
   ```

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204120146850.png" />

3. Install more dependencies

   ```bash
   $ python3 -V
   $ sudo apt install -y python3-pip
   $ sudo apt-get install build-essential
   $ sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
   ```

   

4. Pip installations

   ```bash
   $ pip3 install scikit-build
   $ pip3 install --upgrade pip
   $ pip3 install opencv-python
   $ pip3 install matplotlib
   $ pip3 install imutils
   $ pip3 install pyautogui
   
   $ pip3 install gym
   $ pip3 install pybullet
   ```



5. Install `git` and clone `pybullet` repos

   ```bash
   $ sudo apt install git
   $ sudo apt update
   $ sudo apt install idle3
   
   $ git clone https://github.com/bulletphysics/bullet3
   $ git clone https://github.com/erwincoumans/pybullet_robots.git
   ```

   

6. Testing

   ```bash
   $ cd pybullet_robots
   $ python3 atlas.py
   ```

   

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220204121654119.png" />



## ROS Installation



Follow installation for ROS Noetic from the website: http://wiki.ros.org/noetic/Installation/Ubuntu

```bash
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

$ sudo apt install curl # if you haven't already installed curl
$ curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

$ sudo apt update
$ sudo apt install ros-noetic-desktop-full
$ source /opt/ros/noetic/setup.bash
$ echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
$ source ~/.bashrc
$ sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential

$ sudo apt install python3-rosdep
$ sudo rosdep init
$ rosdep update
```



## Robotics Toolbox - Python

1. Clone repo:

   ```bash
   $ git clone https://github.com/petercorke/robotics-toolbox-python.git
   ```

2. Install libraries

   ```bash
   $ pip3 install roboticstoolbox-python
   $ pip3 install sympy
   ```

3. Execute python script

   ````bash
   $ cd robotics-toolbox-python/roboticstoolbox/examples
   $ python plot.py
   ````

4. Result:

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220111132706203.png" alt="image-20220111132706203" style="zoom: 67%;" />



### Swift installation

```bash
$ pip3 install swift-sim
```

```bash
$ git clone https://github.com/jhavl/swift.git
$ cd swift
$ pip3 install -e .
```



```bash
$ cd robotics-toolbox-python/roboticstoolbox/examples
$ idle
```


Open `dual_mobile_robot.py`

<img src="https://github.com/robogeekcanada/winter_2022/blob/main/images/image-20220201105732944.png" />

