# README #

Bluetooth LE PC server. Project aims to help in BLE devise development. 

### Check for BLE support in your Linux ###

```
hciconfig -a

HCI Version: 4.0 (0x6)  Revision: 0x1000

```

then cheking HCI Version, mine says 0x6 that's version 4.0 so my computer supports BLE.
BLE is part of Bluetooth 4.0 and higher as you basically stated


### BLE terminology ###

* [GAP](https://learn.adafruit.com/introduction-to-bluetooth-low-energy/gap) is an acronym for the Generic Access Profile, and it controls connections and advertising in Bluetooth. GAP is what makes your device visible to the outside world, and determines how two devices can (or can't) interact with each other.
* [GATT](https://learn.adafruit.com/introduction-to-bluetooth-low-energy/gatt) comes into play once a dedicated connection is established between two devices, meaning that you have already gone through the advertising process governed by GAP.


### Bring up Linux BLE dev environment ###

Thanks to [post](http://stackoverflow.com/questions/29128586/bluetooth-low-energy-in-c-using-bluez-to-create-a-gatt-server?answertab=active#tab-top) 

```
sudo apt-get update
sudo apt-get install --install-recommends linux-generic-lts-vivid
sudo apt-get install libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev

```

Checkout and step into project

```
git clone git@bitbucket.org:ubox/ble_emulator.git
cd ble_emulator
```


Then to download and build latest bluez code. This project tested with bluez-5.41.tar.xz  

```
wget https://www.kernel.org/pub/linux/bluetooth/bluez-5.41.tar.xz  
tar xvf bluez-5.31.tar.xz
cd bluez-5.31
./configure --prefix=/usr --mandir=/usr/share/man --sysconfdir=/etc --localstatedir=/var --disable-systemd --enable-experimental --enable-maintainer-mode
make
sudo make install
sudo cp attrib/gatttool /usr/bin
```

Installation completed.

### Test Low Energy GATT server example ###

cd to Downloaded Bluez5.41 directory then

```

sudo tools/btmgmt -i hci0 power off
sudo tools/btmgmt -i hci0 le on
sudo tools/btmgmt -i hci0 connectable on
sudo tools/btmgmt -i hci0 name "some friendly name"
sudo tools/btmgmt -i hci0 advertising on
sudo tools/btmgmt -i hci0 power on
tools/btgatt-server -i hci0 -s low -t public -r -v

```

Go to another device (I've used an iPod, an Android -- Samsung Galaxy 5S and Nexus tablet -- and another PC running BlueZ) and connect to the service. Here is how I did it on another PC running BlueZ:
```
gatttool -b MAC address of GATT server -I
connect
primary
characteristics
```

### Build BLE emulator ###

work directory has structure like below

├── bluez-5.41
├── CMakeLists.txt
├── README.md
└── src

```
cmake .
make
```

then run your Noutbook into pereferial devise mode

./ble_emulator
