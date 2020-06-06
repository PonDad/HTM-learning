# htm.core on RaspberryPi4 + 64 bit RaspberryPi OS

How to install htm.core on RaspberryPi4.

## Preinstalled Image Download and Burn

Download the unofficial image from this link.

[Raspberry Pi OS (64 bit) beta test version](https://www.raspberrypi.org/forums/viewtopic.php?f=117&t=275370&fbclid=IwAR0YAbnFVdmKMb1of7UMAVWTtksFk5akMTgubS6a2XGzdY0vx9lD7XBDj78)

flashing an 32GB SD card.

[BalenaEtcher](https://www.balena.io/etcher/)

## Install htm.core

Refer to offical repository.

[htm-community/htm.core](https://github.com/htm-community/htm.core)

**`.bashrc`**

![1-2](https://github.com/PonDad/My-HTM-learning/blob/master/appendix-2/images/1-2.png?raw=true)

add `export ARCHFLAGS="-arch arm64"` to the `.bashrc` file.

```bash
export ARCHFLAGS="-arch arm64"
```

and

```bash
$ sudo apt update
$ sudo reboot
```

**cmake**

`sudo python3 -m pip install cmake>=3.10`installation error.

[Installing cmake on aarch64 using pip via wheel](https://github.com/scikit-build/cmake-python-distributions/issues/96)

```bash
$ sudo pip3 install scikit-build
$ sudo apt install cmake
```
```bash
$ git clone https://github.com/scikit-build/cmake-python-distributions
$ cd cmake-python-distributions
$ sudo pip3 install -r requirements-dev.txt
$ sudo python3 setup.py bdist_wheel && ls dist
```
*install time about 15min. ☕

**C++ compiler**

```bash
$ sudo apt install clang
```

**Python build**

Switch from LAN to WiFi (to save memory).Connect with SSH.

```bash
$ cd ~
$ git clone https://github.com/htm-community/htm.core.git
$ cd htm.core
$ sudo python3 setup.py install

```

*build & make & install time about 1H. ☕

```bash
$ python3
>>> import htm
>>> import htm.bindings
>>> exit()

$ sudo pip3 install mock
$ sudo pip3 install hexy
$ sudo pip3 install numpy

$ sudo python3 setup.py test
```

## Install Libraries

**matplotlib**

`sudo apt install python3-matplotlib` installation error.

```bash
$ sudo apt install libfreetype6-dev pkg-config
$ sudo pip3 install matplotlib
```

