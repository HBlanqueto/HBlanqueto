![OS](https://img.shields.io/badge/Unstable-%23E0234E.svg?style=for-the-badge&logo=debian&logoColor=white&style=flat)

In my **Gnome**, I use the Wayland session for multiple reasons of taste, so in this section are some of the configurations that I use and you can apply to share screen, use pipewire among others. 

## Depdendencies ℹ️

```
sudo apt install xdg-desktop-portal-wlr xdg-desktop-portal xdg-desktop-portal-gtk
```

## Chromium Based 🌐

<p align='center'>
	<img src='https://raw.githubusercontent.com/HBlanqueto/HBlanqueto/master/wayland/Sharing_screen.png'/>
</p>

**Enable Screen Sharing**

How to enable it? It is as simple as typing in the address bar "according to the browser" the following that I have below:
⠀⠀⠀⠀

**Google Chrome**
```
chrome://flags/#enable-webrtc-pipewire-capturer
```

**Microsoft Edge**
```
edge://flags/#enable-webrtc-pipewire-capturer
```

**Brave**
```
brave://flags/#enable-webrtc-pipewire-capturer
```

**Opera (not implemented yet)**
```
opera://flags/#enable-webrtc-pipewire-capturer
```

**Enable Wayland**
1. Go to */usr/share/applications/* to find the .desktop file
```
cd /usr/share/applications/
```

2. Find the ".desktop" file in your browser and edit it with your preferred editor. Then add `--enable-features=UseOzonePlatform --ozone-platform=wayland` to the Exec line. Example:

```
Exec=/usr/bin/google-chrome-unstable --enable-features=UseOzonePlatform --ozone-platform=wayland %U
```
## Firefox 🦊

<p align='center'>
	<img src='https://raw.githubusercontent.com/HBlanqueto/HBlanqueto/master/wayland/firefox.png'/>
</p>

**Running Firefox under Wayland**

More recent versions of Firefox support opting into Wayland mode via an environment variable.

```
MOZ_ENABLE_WAYLAND=1 firefox
```

To make this permanent, see Environment variables#Graphical environment and start Firefox via the desktop launcher like you normally would. To verify it worked check the Window Protocol again.

You may enter about:support in the `URL` bar to check the Window Protocol. It should say wayland instead of x11 or xwayland.

On native Wayland Firefox rendering performance can be significantly improved by setting `gfx.webrender.compositor.force-enabled` to `true` in `about:config`. As of Firefox 89, this feature is experimental and Firefox Nightly is recommended for testing.

**Sharing Screen**

If you have all necesary dependencies like xdg-desktop-portal & pipewire, It will be enabled by default

## Flatpak 📦

In case you use Flatpak to install programs I will share you some tips to run native programs on wayland. If you are interested in using Flatpak for daily use [here are my guide to configure it](https://github.com/HBlanqueto/dotsbian/wiki/Flatpak)

**Telegram**
```
sudo flatpak override --env=QT_QPA_PLATFORM=wayland org.telegram.desktop
```

## Pipewire 🔈

<p align='center'>
	<img src='https://raw.githubusercontent.com/HBlanqueto/HBlanqueto/master/wayland/pipewire.png'/>
</p>


I use debian unstable so for this you need the most recent version, if you are in Bullseye I recommend the following [tutorial to install pipewire 3.34](https://salmorejogeek.com/2021/08/29/como-instalar-el-ultimo-pipewire-0-3-34-en-debian-11-bullseye-y-ponerlo-como-server-de-audio-por-defecto/).

**Dependencies**
```
sudo apt install pipewire libpipewire-0.3-0 libpipewire-0.3-common
sudo apt install gstreamer1.0-pipewire libpipewire-0.3-{0,dev,modules} libspa-0.2-{bluetooth,dev,jack,modules} pipewire{,-{audio-client-libraries,pulse,media-session,bin,tests}}
```

**Disable Pulseaudio**
```
systemctl --user --now disable pulseaudio.{socket,service}
systemctl --user mask pulseaudio
```

**Enable & Start pipewire**
```
systemctl --user --now enable pipewire{,-pulse}.{socket,service} pipewire-media-session.service
```

## Sources 📃
- https://wiki.archlinux.org/title/firefox#Wayland
- https://github.com/flathub/org.telegram.desktop/issues/169