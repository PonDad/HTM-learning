# htm.core on RaspberryPi4 + 64 bit Ubuntu 18.04.4 LTS

How to install htm.core on RaspberryPi4.

## Preinstalled Image Download and Install

Refer to this site.

[Raspberry Pi 4 Ubuntu Server/Desktop 18.04.4 Image (unofficial) - James A. Chambers Legendary Technology Blog](https://jamesachambers.com/raspberry-pi-4-ubuntu-server-desktop-18-04-3-image-unofficial/)

Download the unofficial image from this link.

[TheRemote/Ubuntu-Server-raspi4-unofficial](https://github.com/TheRemote/Ubuntu-Server-raspi4-unofficial/releases)

flashing an 32GB SD card.

[BalenaEtcher](https://www.balena.io/etcher/)

Enable Ethanet Network.

[Ubuntuで有線LANで接続しようとしても](https://www.nemotos.net/?p=3123)

```bash
$ cd /etc/NetworkManager/conf.d
$ sudo touch 10-globally-managed-devices.conf
$ sudo service network-manager restart
```

## Install htm.core

Refer to offical repository.

[htm-community/htm.core](https://github.com/htm-community/htm.core)

**`.bashrc`**

![1-2](https://github.com/PonDad/My-HTM-learning/blob/master/appendix-2/images/1-1.png?raw=true)

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

`sudo apt install python3-cmake`build error.

[stackoverflow](https://stackoverflow.com/questions/51154143/not-able-to-install-skbuild)

```bash
$ sudo pip3 install scikit-build
$ sudo pip3 install cmake
```

*install time about 40min. ☕

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

