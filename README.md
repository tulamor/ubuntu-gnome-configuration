# Ubuntu: 20.04 LTS / GNOME 3.36

## Wi-Fi troubleshooting

### Install drivers from ISO  
Download the Ubuntu ISO corresponding to your Ubuntu version  
Place the Ubuntu ISO into the Home directory on Ubuntu  
```bash
sudo mkdir /media/cdrom
sudo mount -o loop ubuntu-*.iso /media/cdrom
```
Go to “Software & Updates”  
Click the “Additional Drivers” tab, then select the “Wireless Network Adapter” option and click “Apply Changes”.  
  
### Finding network adapters (see if device is detected):
```bash
sudo lsusb # <-- if devices connected via USB
sudo lspci # <-- if it is internal device
lshw -C network # <-- test if the machine can see the wireless device
```
### Check if the driver module is not missing
```bash
sudo lsmod # <-- list of modules that are used
sudo modprobe modulename # <-- to activate your module, where “modulename” is the chipset
# sudo modprobe rt2800usb
lsmod <-- see if it has loaded correctly
```
### Make driver module automatically boot
```bash
sudo nano /etc/modules # <-- Add module name
```
### Issues with network manager
```bash
sudo service network-manager restart
sudo apt-get install network-manager
sudo apt install --reinstall gnome-control-center
```
###  If none above works, try to edit configuration file
```bash
sudo nano /etc/network/interfaces
# assert with
auto lo
iface lo inet loopback
 
auto wlan0
iface wlan0 inet dhcp

sudo ifdown wlan0 && sudo ifup -v wlan0  # <-- restart the interface
