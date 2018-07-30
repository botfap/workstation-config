# workstation-config
Ubuntu 18.04 Workstation Setup Guide for IOTFAP Students 2018

## Ubuntu 18.04 IOTFAP Workstation Initial Setup
<iotfap-logo.png>

## 0. Preperation

#### 0.1. Backup the system you will be using BEFORE you start

#### 0.2. Prepare USB Install Media

- Download Ubuntu 18.04 amd64 iso
- Flash to USB drive for hardware install
- Boot system with Ubuntu USB drive and chose Live system, not Install

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

Perform a generic install of Ubuntu 18.04 Desktop, splitting root and home partitions on the primary SSD

#### 1.2. Use manual disk partitioning

- rootfs	ext4	/		SystemHD	12-24GB
- homes	ext4	/home	HomeHD		60GB+
- Install the bootloader to the primary disk

#### 1.3. User Creation

- Disable auto login
- Disable encrypted homes (unless specifically needed)

#### 1.4. Software Selection

Chose:
- normal software install
- 3rd party codecs

#### 1.5. Finish

- Choose the option to reboot and remove USB drive

#### 1.6. Prepare system


```
sudo -s
sed -i 's/# deb http:\/\/archive.canonical.com\/ubuntu bionic partner/deb http:\/\/archive.canonical.com\/ubuntu bionic partner/g' /etc/apt/sources.list
apt update && apt -y upgrade
```

#### 1.7. Remove unwanted packages

```
sudo apt remove --purge thunderbird* totem

sudo rm /usr/share/ubuntu-web-launchers/amazon-launcher /usr/share/applications/com.canonical.launcher.amazon.desktop /usr/share/applications/ubuntu-amazon-default.desktop

snap remove gnome-calculator gnome-characters gnome-logs gnome-system-monitor gnome-3-26-1604

apt install gnome-calculator gnome-characters gnome-logs gnome-system-monitor
```

#### 1.8. Environment Config

```

echo "#QT_QPA_PLATFORMTHEME=qt5ct" >> .bashrc

mkdir .local/bin
```

#### 1.9. Enable Pop_OS, Yandex Disk repo, Update & Reboot


```
wget http://repo.yandex.ru/yandex-disk/YANDEX-DISK-KEY.GPG -O- | sudo apt-key add - 

wget http://repo.yandex.ru/yandex-disk/yandex-disk_latest_amd64.deb && sudo dpkg -i yandex-disk_latest_amd64.deb && rm -f yandex-disk_latest_amd64.deb

sudo add-apt-repository -y ppa:slytomcat/ppa

sudo add-apt-repository ppa:gambas-team/gambas3

sudo add-apt-repository -y ppa:system76/pop

sudo apt update && sudo apt -y upgrade

```


## 2. Setup base software environment
#### 2.1. Install base system & dev tools tools

```
sudo apt install -y htop system-config-samba synaptic screen dialog tilix vim-gtk3 synaptic putty samba unzip bc openssh-server wireshark-gtk 

sudo apt install -y build-essential git ncurses-dev qemu-system-arm qemu-system-x86 qemu-system-i386 qemu-utils libssl-dev libelf-dev bison flex gitg meld popsicle bluefish geany* sqlitebrowser mysql-workbench gambas3

sudo apt install -y gtk3-engines-breeze breeze-gtk-theme ttf-mscorefonts-installer libreoffice-style-sifr gtk-theme-switch pop-icon-theme pop-icon-theme-extra pop-fonts pop-wallpapers pop-gnome-shell-theme pop-session pop-theme pop-shop breeze-cursor-theme breeze-gtk-theme breeze gtk3-engines-breeze gnome-tweak-tool gtk-theme-switch qt5ct qt5-style-plugins youtube-dl gedit-developer-plugins

sudo apt install -y gnome-shell-extension-dash-to-panel gnome-shell-extension-dashtodock gnome-shell-extension-hide-veth gnome-shell-extension-disconnect-wifi gnome-shell-extension-redshift redshift gnome-shell-extensions-gpaste gpaste gnome-shell-extension-appindicator gnome-shell-extension-system-monitor gnome-shell-extension-log-out-button gnome-shell-extension-trash gnome-video-effects-extra gnome-video-effects gnome-shell-extension-caffeine gnome-shell-extension-no-annoyance gnome-shell-extension-remove-dropdown-arrows

sudo apt install -y evolution evolution-ews mail-notification-evolution evolution-rss libreoffice-evolution telegram-desktop yandex-disk yd-tools vlc popsicle-gtk glabels  filezilla gimp gimp-data-extras audacity kolourpaint inkscape inkscape-open-symbols glabels geary

#### 2.2. Install IOTFAP Standard Ubuntu Desktop Env

```
```


#### 2.3. Install & License VMWare Workstation Pro 14

```
wget http://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-14.1.2-8497320.x86_64.bundle && chmod +x VMware-Workstation-Full-14.1.2-8497320.x86_64.bundle

sudo ./VMware-Workstation-Full-14.1.2-8497320.x86_64.bundle

rm -f VMware-Workstation-Full-14.1.2-8497320.x86_64.bundle
```

#### 2.5. Install & License SSHCRT

```
wget https://raw.githubusercontent.com/botfap/workstation-config/master/pkgs/sshcrt.txz

tar -xf sshcrt.txz

sudo dpkg -i sshcrt/*.deb

sudo sshcrt/sshcrt.pl /usr/bin/Sec*

sudo apt -f install
```

#### 2.6. Install Remarkable

```
wget https://remarkableapp.github.io/files/remarkable_1.87_all.deb && sudo dpkg -i remarkable_1.87_all.deb

sudo apt install -f && rm -f remarkable_1.87_all.deb
```

#### 2.7. Install Google Chrome
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

sudo dpkg -i google-chrome-stable_current_amd64.deb

sudo apt install -f
```

#### 2.8. Install and arc-menu from the Kubuntu software centre


#### 2.9. Update & Reboot

```
sudo apt update

sudo apt upgrade

sudo reboot
```


## 3. Setup home environment

V1.2, botfap, Friday, 27. April 2018 09:12pm 
