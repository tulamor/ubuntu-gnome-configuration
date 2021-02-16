# Ubuntu: 20.04 LTS / GNOME 3.36

sudo apt-get update; sudo apt-get upgrade

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
```

### Disable telemetry
```bash
ubuntu-report -f send no
sudo apt-get autoremove ubuntu-report popularity-contest
sudo apt-get autoremove unity-lens-shopping
```
### Enable firewall
```bash
sudo ufw enable
sudo ufw status verbose
sudo ufw status numbered
```

## Applications to install
```
vlc
trash-cli  # Add alias rm=trash to your .zshrc/.bashrc to reduce typing & safely trash files
neofetch   # CLI tool to display sysinfo
htop
gparted    # Graphical tool for managing disks on Linux
ubuntu-restricted-extras # Media codecs to support non-free formats
timeshift  # System restore utility
preload    # Cashes most used apps (quick start for most used apps)
gnome-tweaks
synaptic   # GTK-based graphical user interface for the APT package manager
jitsi      # Collection of voice, video conferencing and messaging applications for the web platform
use custom DNS (inside connection settings add custom DNS google / cloudflare)
App Launcher > Privacy > Disable Diagnostics send error reports / Location / Problem reporting / Connectivity checking


firefox settings:
about:config
layers.acceleration.force-enabled > True # enables hardware acceleration
gfx.webrender.all > True
```

##  Applications to try
```
chromium
brave
libre office
gimp
stacer  # system monitoring / cleaning cache
BleachBit
notepadqq
vimtutor
kdenlive
simplenote
gnome tweaks # gnome costumization
pdfsam  # manipulate PDF
gnome-shell-extensions # browse extensions.gnome.org
```
## Shortcut keys
`Super + NUM (NUM is the index of application which is pinned to "favorites")`

