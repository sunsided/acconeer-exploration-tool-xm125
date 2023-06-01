# Acconeer Exploration Tool + XM125 / XE125 / A121

You can use the provided [environment.yml](environment.yml) and skip the Exploration Tool
installation below. All other steps are still required.

```shell
mamba env create -f environment.yml
conda activate acconeer
```

## Installation

Install the [Acconeer Exploration Tool](https://github.com/acconeer/acconeer-python-exploration):

```shell
python -m pip install --upgrade acconeer-exptool[app]
```

## Setup

Set up the UART access:

```shell
python -m acconeer.exptool.setup
```

For Ubuntu, this is what will happen:

```
==== Setting up 'Ubuntu_20.04' will do the following:

> Setup up permissions needed for UART communication by adding the current user to the 'dialout' group.
$ sudo usermod -a -G dialout markus

> Create an udev rule for SPI communication with XM112.
Will make sure that /etc/udev/rules.d/50-ft4222.rules contains this content:

    'SUBSYSTEM=="usb", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="601c", MODE:="0666"\n'


> Create an udev rule for USB communication with XC120.
Will make sure that /etc/udev/rules.d/50-xc120.rules contains this content:

    'SUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="a41d", MODE:="0666"\nSUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="a42c", MODE:="0666"\nSUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="a42d", MODE:="0666"\nSUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="a449", MODE:="0666"\n'


> Download dependencies via "apt" that are required to run the Exploration tool app.
$ sudo apt update
$ sudo apt install -y libxcb-xinerama0-dev libusb-1.0-0

> Trigger udev to update the permission rules.
$ sudo udevadm control --reload-rules
$ sudo udevadm trigger
```

## Flashing / Setting up the XM125

See [Setting up your XM125](https://docs.acconeer.com/en/latest/exploration_tool/evk_setup/xm125.html):

```shell
python -m acconeer.exptool.flash flash -d XM125 -f
```

## Launching the app

Run the Exploration Tool:

```shell
python -m acconeer.exptool.app
```
