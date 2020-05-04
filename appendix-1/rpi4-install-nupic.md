# NuPIC on RaspberryPi4 + 64 bit Ubuntu 18.04.4 LTS

NuPIC on RaspberryPi.

## Preinstalled Image Download and Install

Refer to this site.

[Raspberry Pi 4 Ubuntu Server / Desktop 18.04.4 Image (unofficial) - James A. Chambers Legendary Technology Blog](https://jamesachambers.com/raspberry-pi-4-ubuntu-server-desktop-18-04-3-image-unofficial/)

Download the unofficial image from this link.

[TheRemote / Ubuntu-Server-raspi4-unofficial](https://github.com/TheRemote/Ubuntu-Server-raspi4-unofficial/releases)

## Install NuPIC

Refer to this forum.

[NuPIC on Raspberry Pi 2(rev 1.2)/ 3B/ B+ with Xubuntu - HTM FORUM](https://discourse.numenta.org/t/nupic-on-raspberry-pi-2-rev-1-2-3b-b-with-xubuntu/4550)

If you work with this reference, you can install it.

However, please note that the location is different from the following one.

```
Edit Output.hpp:
nano $NUPIC_CORE/src/nupic/engine/Output.hpp

And add “noexcept(false)” to line 62:
~Output() noexcept(false);
```

You should be able to run the sample code.

```bash
$ python /nupic/examples/sp/hello_sp.py
```

## Install Libraries

How to install a library that gives an installation error.

test