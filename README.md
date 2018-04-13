# LB-LINK-H16
This driver supports Ralink / Mediatek mt766u, mt7632u and mt7612u chipsets.

In particular, the driver supports several USB dongles such as LB-LINK-H16, Netgear-A6210,ASUS USB-AC55, ASUS USB-N53 and EDUP EP-AC1601. 

To build the driver, follow these steps:

    $ git clone https://github.com/leedexun/LB-LINK-H16.git
    $ cd LB-LINK-H16
    $ make
    $ sudo make install

The driver is mostly tested on 64 bit Ubuntu 14.10 (kernel 4.2.0) with LB-LINK-H16 High Gain Wifi USB Adapter. 
Some other distro/dongle combinations work as well, for example
Linux Mint 17.3 "Rosa" - KDE (32-bit)/ASUS USB-N53 seems to work flawlessly
(as reported by Roland Bauer).

The supported chipsets can be present in other devices. To include additional 
devices, you need to add corresponding VendorID, DeviceID into the file 
"rtusb_dev_id.c"

The original code was downloaded from: 
http://cdn-cw.mediatek.com/Downloads/linux/MT7612U_DPO_LinuxSTA_3.0.0.1_20140718.tar.bz2

This is work in progress. The driver is functional. However, there are still
several issues that need to be addressed. In particular, hot-unplugging may
cause the network manager to become unreliable. After plugging the dongle back in, 
you may need to restart the manager:

    $ sudo service network-manager restart

This seems to be Linux distro dependent, but definitely observed on Ubuntu.

EDUP EP-AC1601 works (or to be precise, should work), but at present there are
several problems such as frequent dropping of connection, failure to connect, wildly 
oscillating signal strength etc. This also seems to depent on the Linux distro

	#dkms install to be fixed

after install this driver, you need to use usb_modeswitch to change this device from usbstorage to usbnet, you can finish it with 40-usb_modeswitch.rules.for my ubuntu, it's locate in lib/udev/rules.d/40-usb_modeswitch.rules

