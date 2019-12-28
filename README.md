# Guide-Manjaro-KDE

manjaro-kde-18.0-rc1-stable-x86_64 or new version.

![Image](https://github.com/oguzkaganeren/dell7559-Manjaro-KDE/blob/master/Screenshot_20181103_095750.png)

```
sudo nano /etc/default/grub 
```
> GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_osi=! acpi_osi=\"Windows 2009\" acpi_backlight=vendor i915.modeset=1 scsi_mod.use_blk_mq=1" 
```
update-grub
```
### Update the system
```
pamac update
```
### Packages I use(include aur packages)
```
pamac install yay aria2 speedtest-cli telegram-desktop kdenlive inkscape create_ap virtualbox fish flameshot deepin-terminal neofetch gtop kolourpaint gedit materia-theme opera chromium ttf-font-awesome ttf-font-awesome-4 ttf-roboto android-studio woeusb-git jdownloader2 ttf-ms-fonts vscodium-bin breeze-blurred-git otf-san-francisco xdman gwe svr zettlr-bin fslint odio-appimage skypeforlinux-stable-bin posy-cursors all-repository-fonts ttf-wps-fonts keepassxc

```


### Remove Kate(I don't like it). I use gedit
```
sudo pacman -Rns kate
```
### Change the shell
```
chsh -s /usr/bin/fish
curl -L https://get.oh-my.fish | fish
```
### Power settings(optional)
About: https://forum.manjaro.org/t/howto-power-savings-setup-20180906/1445



### For Other Partitations
If you have another partition(E, D etc.). You can mount it on the startup. Thus some applications which are using other partitions don't get an error.

```
lsblk -f
```
The command shows your disks uuid.
```
sudo gedit /etc/fstab 
```
Open your fstab config with the command. You should add codes similar to the following example. You should change UUID and /run/media/yourUserName/Partition.
```
UUID=b336b98e-d0b5-4254-b6aa-9e66f85b0dfc /run/media/oguz/Files ext4 defaults  0 0
```

>  :exclamation: If you use manjaro with dual boot, you should close fast-startup,hibarnate on your Windows, otherwise, you have not a write permission for other partitions.

### Installing Nvidia Drivers
Open System Settings or Manjaro Settings>Drivers, then click Auto Install Proprietary Drivers.


After Installing restart your computer. Done.
### Firefox screen tearing during scrolling Issue
```
sudo gedit /etc/profile.d/kwin.sh
```
then put this in it,
```
#!/bin/sh

export KWIN_TRIPLE_BUFFER=1
```
After that, 
```
sudo gedit ~/.config/kwinrc
```
Add those parameters at the bottom,

```
MaxFPS=60
RefreshRate=60
```
Save it and reboot. 
Open firefox and 
**about:config**
then search  **layers.acceleration.force-enabled**
It should be true.
Done.
### If you want to edit your host file
```
sudo gedit /etc/hosts
```
>  :exclamation: If you have a SSD, you should enable fstrim.
```
sudo systemctl enable fstrim.timer
```
### Open Wifi Hotspot
```
sudo create_ap wlp5s0 wlp5s0 MyAccessPoint password
```
## Optional
### Fastest Mirror List
```
sudo pacman-mirrors --fasttrack 5
```
### Colorful Yay
```
sudo gedit /etc/pacman.conf
```
Change `#Color` to `Color` below the Music options.
### Terminal PS1
```
sudo gedit .bashrc
```
Change PS1 with this;
```
PS1='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \[\033[0;32m\]$(git_branch)\n\[\033[0;32m\]└─\t\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '
```
and add this lines at the bottom;
```
git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
```
![Image](https://user-images.githubusercontent.com/5963437/46868048-baf1e580-ce2f-11e8-97aa-a02be1b8a066.png)
### Latte-Dock
If you want to panel which like first image, you should install latte-dock.
```
sudo pacman -S latte-dock
latte-dock
```
You can edit the dock with right click on it.(You can add programs shortcut with drag-drop.)
#### For shortcut(Windows key) for the dock
Right click on the dock and Layout>Plasma, then open terminal
```
kwriteconfig5 --file ~/.config/kwinrc --group ModifierOnlyShortcuts --key Meta "org.kde.lattedock,/Latte,org.kde.LatteDock,activateLauncherMenu"
qdbus org.kde.KWin /KWin reconfigure
```
Done. After that, you can open application launcher with Windows key.

### Installing Arc Theme
```
sudo pacman -S arc-kde kvantum-theme-arc
```
Open Kvantum manager and change theme with arc theme. After that change theme with kvantum at settings.


### For Backup
```
sudo pacman -S timeshift
```
### DVD/CD Mounting
If you have a external CD/DVD,
```
sudo pacman -S k3b
```
### PostgreSQL(for me)
```
sudo pacman -S postgresql
sudo su postgres -l # or sudo -u postgres -i
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
exit
sudo systemctl enable --now postgresql.service
sudo pacman -S pgadmin4

```
## Some Errors and fixer
### Virtualbox
#### NS_ERROR_FAILURE (0x80004005) Error
```
Result Code: 
NS_ERROR_FAILURE (0x80004005)
Component: 
MachineWrap
Interface: 
IMachine {85cd948e-a71f-4289-281e-0ca7ad48cd89}
```
This is the error and we can fix it with this;
```
sudo pacman -Syyu
sudo pacman -S virtualbox-host-dkms
sudo pacman -S linux-headers
sudo modprobe vboxdrv
sudo /sbin/rcvboxdrv setup
```
#### VirtualBox: Error -610 in supR3HardenedMainInitRuntime!
This is the error.
```
VirtualBox: Error -610 in supR3HardenedMainInitRuntime!
VirtualBox: dlopen("/usr/lib/virtualbox/VBoxRT.so",) failed: <NULL>

VirtualBox: Tip! It may help to reinstall VirtualBox.
```
Maybe it can fix with(I didn't try it);
```
sudo chmod -002 /usr/lib/virtualbox
```
Or, I fix it with;
```
sudo chmod -002 /usr
```
