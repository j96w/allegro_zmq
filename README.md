# Allegro Hand ZMQ Interface
Adapted from https://github.com/simlabrobotics/allegro_hand_linux_v4

This interface allows communication with a v4 Allegro hand via ZMQ on the NUC of a Panda Franka robotic arm.

# Required hardware
1. [Allegro hand v4](http://wiki.wonikrobotics.com/AllegroHandWiki/index.php/Allegro_Hand_v4.0)
2. [PCAN-USB interface](https://www.peak-system.com/PCAN-USB.199.0.html?&L=1)

# Setup instructions
## Prerequisites
### 1. PCAN-USB driver
Download, build, and install PCAN-USB driver for Linux "libpcan"
```bash
tar -xzvf peak-linux-driver-x.x.tar.gz
cd peak-linux-driver-x.x
make NET=NO
sudo make install
```
#### Troubleshooting
* If encounter 
  ```bash
  src/pcan-settings.c:47:10: fatal error: popt.h: No such file or directory
     47 | #include <popt.h>
      |      	^~~~~~~~
  compilation terminated.
  ```
  Run
  ```bash
  sudo apt install libpopt-dev
  ```

### 2. `libpcanbasic`
Download, build, and install PCAN-Basic API for Linux: libpcanbasic
```bash
tar -xzvf PCAN_Basic_Linux-x.x.x.tar.gz
cd PCAN_Basic_Linux-x.x.x/pcanbasic
make
sudo make install
```

### 3. `libBHand` grasping library
Download, build, and install Grasping Library for Linux, "libBHand": Grasping_Library_for_Linux
```bash
unzip LibBHand_{32|64}.zip
cd libBHand_{32|64}
sudo make install
sudo ldconfig
```


## Installing this interface
Build using cmake "out of source build" style.
```bash
cd allegro_zmq
mkdir build && cd build
cmake ..
make
make install
```

# Usage
## Launching the interface
1. Connect PCAN-USB and Allegro Hand (connect to the NUC of franka robot)
1. Power on the Allegro Hand.
1. Start the grasping program: "grasp": `build/bin/grasp` on the NUC. You should see the configuration of your hand print out.

## Controlling via ZMQ
`ws_control.py` is an example code that runs on a workstation using Python. Make sure to replace `localhost` with the correct IP address of the NUC in this code.