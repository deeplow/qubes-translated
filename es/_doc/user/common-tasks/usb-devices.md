---
lang: es
layout: doc
permalink: /es/doc/usb-devices/
redirect_from:
- /es/doc/usb/
ref: 195
title: USB Devices
---

# USB Devices
<a id="usb-devices"></a>

*This page is part of [device handling in qubes].*

If you are looking to handle USB *storage* devices (thumbdrives or USB-drives), please have a look at the [block device] page.

**Note:** Attaching USB devices to VMs requires a [USB qube][USB-qube howto].

**Important security warning:** USB passthrough comes with many security implications.
Please make sure you carefully read and understand the **[security considerations]**.
Whenever possible, attach a [block device] instead.

Examples of valid cases for USB-passthrough:

- [microcontroller programming]
- [external audio devices]
- [optical drives] for recording

(If you are thinking to use a two-factor-authentication device, [there is an app for that][qubes u2f proxy].
But it has some [issues][4661].)

## Attaching And Detaching a USB Device
<a id="attaching-and-detaching-a-usb-device"></a>

### With Qubes Device Manager
<a id="with-qubes-device-manager"></a>

Click the device-manager-icon: ![device manager icon]
A list of available devices appears.
USB-devices have a USB-icon to their right: ![usb icon]

Hover on one device to display a list of VMs you may attach it to.

Click one of those.
The USB device will be attached to it.
You're done.

After you finished using the USB-device, you can detach it the same way by clicking on the Devices Widget.
You will see an entry in bold for your device such as **`sys-usb:2-5 - 058f_USB_2.0_Camera`**.
Hover on the attached device to display a list of running VMs.
The one to which your device is connected will have an eject button ![eject icon] next to it.
Click that and your device will be detached.

### With The Command Line Tool
<a id="with-the-command-line-tool"></a>

In dom0, you can use `qvm-usb` from the commandline to attach and detach devices.

Listing available USB devices:

```shell_session
[user@dom0 ~]$ qvm-usb
BACKEND:DEVID   DESCRIPTION                    USED BY
sys-usb:2-4     04ca:300d 04ca_300d
sys-usb:2-5     058f:3822 058f_USB_2.0_Camera
sys-usb:2-1     03f0:0641 PixArt_HP_X1200_USB_Optical_Mouse
```

Attaching selected USB device:

```shell_session
[user@dom0 ~]$ qvm-usb attach work sys-usb:2-5
[user@dom0 ~]$ qvm-usb
BACKEND:DEVID   DESCRIPTION                    USED BY
sys-usb:2-4     04ca:300d 04ca_300d
sys-usb:2-5     058f:3822 058f_USB_2.0_Camera  work
sys-usb:2-1     03f0:0641 PixArt_Optical_Mouse
```

Now, you can use your USB device (camera in this case) in the `work` qube.
If you see the error `ERROR: qubes-usb-proxy not installed in the VM` instead, please refer to the [Installation Section].

When you finish, detach the device.

```shell_session
[user@dom0 ~]$ qvm-usb detach work sys-usb:2-5
[user@dom0 ~]$ qvm-usb
BACKEND:DEVID   DESCRIPTION                    USED BY
sys-usb:2-4     04ca:300d 04ca_300d
sys-usb:2-5     058f:3822 058f_USB_2.0_Camera
sys-usb:2-1     03f0:0641 PixArt_Optical_Mouse
```

## Maintenance And Customisation
<a id="maintenance-and-customisation"></a>

### Creating And Using a USB qube
<a id="creating-and-using-a-usb-qube"></a>

If you've selected to install a usb-qube during system installation, everything is already set up for you in `sys-usb`.
If you've later decided to create a usb-qube, please follow [this guide][USB-qube howto].

### Installation Of `qubes-usb-proxy`
<a id="installation-of-qubes-usb-proxy"></a>

To use this feature, the `qubes-usb-proxy` package needs to be installed in the templates used for the USB qube and qubes you want to connect USB devices to.
This section exists for reference or in case something broke and you need to reinstall `qubes-usb-proxy`.
Under normal conditions, `qubes-usb-proxy` should already be installed and good to go.

If you receive this error: `ERROR: qubes-usb-proxy not installed in the VM`, you can install the `qubes-usb-proxy` with the package manager in the VM you want to attach the USB device to.

- Fedora: `sudo dnf install qubes-usb-proxy`
- Debian/Ubuntu: `sudo apt-get install qubes-usb-proxy`

### Using USB Keyboards And Other Input Devices
<a id="using-usb-keyboards-and-other-input-devices"></a>

**Warning:** especially keyboards need to be accepted by default when using them to login! Please make sure you carefully read and understood the **[security considerations]** before continuing!

Mouse and keyboard setup are part of [setting up a USB-qube][keyboard setup].

### Finding The Right USB Controller
<a id="finding-the-right-usb-controller"></a>

Some USB devices are not compatible with the USB pass-through method Qubes employs.
In situations like these, you can try to pass through the entire USB controller to a qube as PCI device.
However, with this approach one cannot attach single USB devices but has to attach the whole USB controller with whatever USB devices are connected to it.

If you have multiple USB controllers, you must first figure out which PCI device is the right controller.

First, find out which USB bus the device is connected to (note that these steps need to be run from a terminal inside your USB qube):

```
lsusb
```

For example, I want to attach a broadband modem to the NetVM.
In the output of `lsusb` it may be listed as something like:

```
Bus 003 Device 003: ID 413c:818d Dell Computer Corp.
```

(In this case, the device isn't fully identified)

The device is connected to USB bus \#3.
Check which other devices are connected to the same bus, since *all* of them will be attach to the same VM.

To find the right controller, follow the usb bus:

```
readlink /sys/bus/usb/devices/usb3
```

This should output something like:

```
../../../devices/pci-0/pci0000:00/0000:00:1a.0/usb3
```

Now you see the path and the text between `/pci0000:00/0000:` and `/usb3` i.e. `00:1a.0` is the BDF address. Strip the address and pass it to the [`qvm-pci` tool][qvm-pci] to attach the controller to the targetVM.

For example, On R 4.0 the command would look something like

`qvm-pci attach --persistent personal dom0:00_1a.0`

[device handling in qubes]: /es/doc/device-handling/
[block device]: /es/doc/block-devices/
[security considerations]: /es/doc/device-handling-security/#usb-security
[usb-challenges]: https://blog.invisiblethings.org/2011/05/31/usb-security-challenges.html
[usb icon]: /attachment/wiki/Devices/generic-usb.png
[microcontroller programming]: https://www.arduino.cc/en/Main/Howto
[external audio devices]: /es/doc/external-audio/
[optical drives]: /es/doc/recording-optical-discs/
[qubes u2f proxy]: /es/doc/u2f-proxy/
[4661]: https://github.com/QubesOS/qubes-issues/issues/4661
[device manager icon]:/attachment/wiki/Devices/media-removable.png
[eject icon]:/attachment/wiki/Devices/media-eject.png
[Installation Section]:#installation-of-qubes-usb-proxy
[USB-qube howto]: /es/doc/usb-qubes/
[keyboard setup]: /es/doc/usb-qubes/#enable-a-usb-keyboard-for-login
[qvm-pci]: /es/doc/pci-devices/