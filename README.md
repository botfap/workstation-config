# workstation-config
Ubuntu 18.04 Workstation Setup Guide for IOTFAP Students 2018

## Ubuntu 18.04 IOTFAP Workstation Initial Setup
<iotfap-logo.png>

## 0. Preperation

#### 0.1. Backup the system you will be using BEFORE you start

#### 0.2. Prepare USB Install Media

- Download Kbuntu 18.04 amd64 iso
- Flash to USB drive for hardware install
- Boot system with Kubuntu USB drive and chose Live system, not Install

#### 0.3. Check system hardware compatibility

In the live environment make sure all the hardware you need is working as expected. Check at least:

- wifi & ethernet
- graphics
- sound
- webcam
- any other devices you use

#### 0.4 Secure Erase System SSD to restore performance

In the live environment:

- Suspend system to RAM, wait 5 seconds, wake backup (clears ssd security frozen attribute)
- Set ssd security password for secure erase

```
hdparm --security-set-pass 1234 /dev/hda
```

- Secure erase the ssd

```
hdparm --security-erase 1234 /dev/hda
```


## 1. Install Ubuntu 18.04

#### 1.1. Install Ubuntu with Minimal Install except as follows:

Perform a generic minimal of Kbuntu 18.04 Desktop, splitting root and home partitions on the primary disk

#### 1.2. Use manual disk partitioning

- rootfs	ext4	/		SystemHD	12-24GB
- homes	ext4	/home	HomeHD		60GB+
- Install the bootloader to the primary disk

#### 1.3. User Creation

- Disable auto login
- Disable encrypted homes (unless specifically needed)

#### 1.4. Software Selection

Chose:
- minimal software install
- 3rd party codecs

#### 1.5. Finish

- Choose the option to reboot and remove USB drive

#### 1.6. Prepare system

- login to system
- connect network connection
- Enable Canonical Partner Repo
- update system

#### 1.7. Remove unwanted packages

```
sudo apt remove --purge kate* okular* kcalc kde-spectacle muon kwallet* skanlite gwenview k3b* plasma-discover
sudo rm /usr/share/ubuntu-web-launchers/amazon-launcher /usr/share/applications/com.canonical.launcher.amazon.desktop /usr/share/applications/ubuntu-amazon-default.desktop
```

#### 1.8. Environment Config
echo '%botfap   ALL=(ALL:ALL) NOPASSWD:ALL' > /etc/sudoers.d/botfap
echo "QT_QPA_PLATFORMTHEME=qt5ct" >> .profile
mkdir .local/bin

#### 1.9. Enable Pop_OS repo, Update & Reboot
```
sudo add-apt-repository -y ppa:system76/pop
sudo apt update && sudo apt -y upgrade
```


## 2. Setup base software environment
#### 2.1. Install base system & dev tools tools

```
sudo apt install -y htop system-config-samba synaptic screen dialog tilix vim-gnome synaptic putty samba unzip bc openssh-server

sudo apt install -y build-essential git ncurses-dev qemu-system-arm qemu-system-x86 qemu-system-i386 qemu-utils libssl-dev libelf-dev bison flex

sudo apt install -y bluefish geany* mysql-workbench gedit-developer-plugins
``` 

#### 2.2. Install IOTFAP Standard Ubuntu Desktop Env

```
sudo apt install -y pop-desktop gtk3-engines-breeze gnome-tweak-tool gnome-shell-extension-dash-to-panel gnome-shell-extension-dashtodock evolution-ews mail-notification-evolution evolution-rss libreoffice-evolution evolution ttf-mscorefonts-installer libreoffice-style-sifr ubuntu-software gnome-shell-extensions gnome-shell-extension-top-icons-plus gnome-shell-extension-shortcuts gnome-shell-extension-hide-veth gnome-shell-extension-better-volume pop-icon-theme-extra gnome-shell-extension-disconnect-wifi gnome-shell-extension-redshift gnome-shell-extensions-gpaste gnome-shell-extension-workspaces-to-dock gpaste gnome-shell-extension-multi-monitors grub-theme-pop gnome-shell-extension-appindicator gnome-shell-extension-tilix-shortcut gnome-shell-extension-system-monitor gnome-shell-extension-tilix-dropdown redshift gnome-shell-extension-log-out-button gnome-shell-extension-trash gnome-shell-extension-impatience gnome-twitch gtk-theme-switch qt5ct qt5-style-plugins 

sudo apt install -y krita gimp gimp-data-extras audacity kolourpaint inkscape inkscape-open-symbols glabels rhythmbox shotwell
```

#### 2.3. Install & License VMWare Workstation Pro 14

```
wget http://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-14.1.2-8497320.x86_64.bundle
chmod +x VMware-Workstation-Full-14.1.1-7528167.x86_64.bundle
sudo ./VMware-Workstation-Full-14.1.1-7528167.x86_64.bundle
rm wget http://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-14.1.2-8497320.x86_64.bundle
```

#### 2.5. Install & License SSHCRT

```
wget https://raw.githubusercontent.com/botfap/workstation-config/master/pkgs/sshcrt.txz
tar -xf sshcrt.txz
sudo dpkg -i sshcrt/*.deb
sudo sshcrt/sshcrt.pl /usr/bin/Sec*
sudo apt -f install
rm
```

#### 2.6. Install Remarkable

```
wget https://remarkableapp.github.io/files/remarkable_1.87_all.deb
sudo dpkg -i remarkable_1.87_all.deb
sudo apt install -f
rm remarkable_1.87_all.deb
```

#### 2.7. Install Google Chrome
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt install -f
rm google-chrome-stable_current_amd64.deb
```

#### 2.8. Install telegram and arc-menu from the Ubuntu software centre


#### 2.9. Update & Reboot

```
sudo apt update
sudo apt upgrade
sudo reboot
```


## 3. Setup home environment

V1.0, botfap, Friday, 27. April 2018 09:12pm 

