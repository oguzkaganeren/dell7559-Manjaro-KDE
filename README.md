# dell7559-Manjaro-KDE
![Screen](https://github.com/oguzkaganeren/dell7559-Manjaro-KDE/blob/master/Screenshot_20180907_205429.png)
## With oh-my-zsh
![Screen2](https://github.com/oguzkaganeren/dell7559-Manjaro-KDE/blob/master/screen.png)
Install manjaro-kde-17.1.11-stable-x86_64 or new version.

```
sudo nano /etc/default/grub 
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_osi=! acpi_osi=\"Windows 2009\""
```
update-grub
sudo pacman -S --noconfirm --needed git
sudo pacman -S --noconfirm --needed pulseaudio pulseaudio-alsa pavucontrol
sudo pacman -S --noconfirm --needed aria2 git screenfetch ttf-ubuntu-font-family rxvt-unicode unace unrar zip unzip sharutils uudeview arj cabextract speedtest-cli
sudo pacman -S --noconfirm --needed ntp
sudo timedatectl set-ntp true
sudo pacman -S --noconfirm --needed deepin-movie
sudo pacman -S --noconfirm --needed virt-manager qemu vde2 ebtables dnsmasq bridge-utils openbsd-netcat
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
sudo pacman -S --noconfirm --needed tlp tlp-rdw iw smartmontools ethtool x86_energy_perf_policy
sudo systemctl mask systemd-rfkill.socket systemd-rfkill.service
sudo pacman -S --noconfirm --needed lm_sensors && sudo sensors-detect
sudo pacman -S --noconfirm --needed thermald
sudo systemctl enable thermald
sudo systemctl start thermald
yaourt -S whatsapp-web-desktop
yaourt -S materia-theme
yaourt -S opera chromium
yaourt -S spotify ttf-font-awesome ttf-font-awesome-4 powerline-fonts ttf-roboto  adobe-source-sans-pro-fonts android-studio woeusb-git visual-studio-code-bin
sudo pacman -S papirus-icon-theme
yaourt -S gedit
sudo pacman -S ntfs-3g
sudo gedit /etc/fstab 
```
UUID=DAF6FE7CF6FE5869 /run/media/oguz/D ntfs-3g defaults,uid=1000,gid=1000,utf8,umask=0022,rw  0 2
UUID=C480917680917022 /run/media/oguz/E ntfs-3g defaults,uid=1000,gid=1000,utf8,umask=0022,rw  0 2
>  :exclamation: If you use manjaro with dual boot, you should close fast-startup,hibarnate on your Windows, otherwise, you have not a write permission for other partitions.
```
sudo gedit /etc/hosts
```
```
sudo pacman -S arc-kde kvantum-theme-arc
```
Open Kvantum manager and change theme with arc theme. After that change theme with kvantum at settings.

### For Oh-my-Zsh
```
sudo pacman -S zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
yaourt -S powerline-fonts-git  
git clone https://github.com/jeremyFreeAgent/oh-my-zsh-powerline-theme.git
cd oh-my-zsh-powerline-theme
./install_in_omz.sh  
```
Change bash your Konsole in Settings>Conf. Konsole
```

sudo gedit ~/.zshrc
```
ZSH_THEME="powerline"
plugins=(
  git
  cp
  extract
  history
  autojump
  gradle
  node
  npm
  git-flow
  sudo
  zsh-autosuggestions
  tmux
)
