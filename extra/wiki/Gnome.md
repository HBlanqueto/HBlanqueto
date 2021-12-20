[Gnome Desktop Enviroment](https://www.gnome.org/) it's intended to make a Linux operating system easy to use for non-programmers and generally corresponds to the Windows desktop interface and its most common set of applications. In fact, GNOME allows the user to select one of several desktop appearances.

Knowing this, in the Debian GNU/Linux operating system there is the possibility of creating a **"Gnome Minimal"** with a quantity of 750 packages or more depending on what one uses without counting the programs that you use.

## Minimal Packages 📦

Add the next lines in **/etc/apt/apt.conf.d/99local**

```
APT::Install-Suggests "0";
APT::Install-Recommends "0";
```

## Minimal Xorg ❌

*If your gpu is an intel install the next package instead the amdgpu **xserver-xorg-video-intel***

```
sudo apt install --no-install-recommends xserver-xorg-video-amdgpu
sudo apt install --no-install-recommends xserver-xorg-input-libinput
sudo apt install --no-install-recommends xdg-user-dirs
```
## Gnome 👣
```
sudo apt install --no-install-recommends gnome-session
sudo apt install --no-install-recommends fonts-cantarell
sudo apt install --no-install-recommends gdm3
```

Before start the gdm3's process remember to install basic programs

## Basic Programs ⛑️

In my opinion I have very necessary programs and basic services such as:

- **Browser**: Firefox [at least to use it to install some other]
- **File Manager**: Nautilus 
- **Gnome Programs**: Gnome Control Center & Gnome Tweak Tool 
- **Terminal**: Gnome Terminal, Kitty or [Insert your favortite]
- **Sound**: Pulseadio & Pipewire 

**Browser** 🌐

```
sudo apt install firefox-esr
```

**File Manager** 🗃️

```
sudo apt install nautilus gnome-sushi libgdk-pixbuf2.0-bin libpixman-1-0
```

**Gnome Programs** 🔧

```
sudo apt install gnome-control-center gnome-tweak-tool gnome-themes-extra
```

**Terminal** 💻

```
sudo apt install gnome-terminal
```

**Sound** 🔈

If you want to configure and use full pipewire, [please read this](https://github.com/HBlanqueto/dotsbian/wiki/Wayland#pipewire-)
```
sudo apt install pulseadio
systemctl --user --now enable pulseaudio.{socket,service}
```

## NetworkManager 📶
NetworkManager will allow us to use the wifi so the necessary packages to install it would be.
```
sudo apt install network-manager network-manager-gnome 
```

**Enabling Interface Management**

If you want NetworkManager to handle interfaces that are enabled in /etc/network/interfaces:

Set `managed=true in /etc/NetworkManager/NetworkManager.conf`.

Restart NetworkManager:

```
sudo systemctl NetworkManager restart
```

**Wifi Driver**

Depending on the network driver, it is the way in which the drivers will be installed, some taking more time than others, so I will leave you below those that the wiki explains how it would be done

<details><summary><b>iwlwifi</b></summary>

```
sudo apt install firmware-iwlwifi
sudo modprobe -r iwlwifi ; sudo modprobe iwlwifi
sudo systemctl restart NetworkManager.service
```

If you have problems with It, please read the [wiki.debian/iwilwifi](https://wiki.debian.org/iwlwifi)

</details>

<details><summary><b>Broadcom wl</b></summary>

In this case we are going to install dkms 
```
sudo  apt-get install linux-image-$(uname -r|sed 's,[^-]*-[^-]*-,,') linux-headers-$(uname -r|sed 's,[^-]*-[^-]*-,,') broadcom-sta-dkms
sudo apt-get install -f
sudo dpkg-reconfigure broadcom-sta-dkms
```

Load the conflicting modules
```
sudo modprobe -r b44 b43 b43legacy ssb brcmsmac bcma
```

Load the module
```
sudo modprobed wl
sudo systemctl restart NetworkManager.service
```
</details>

## Enable gdm3 🖥️
```
sudo systemctl enable gdm3
```

##

<div align='center'>
  
The tutorial was taken from my friend [AlexisMtzGasca Debootstrap](https://github.com/AlexisMtzGasca/Debootstrap#orge07bcc9)
  
</div>                                            
