Yes, I use Flatpak to avoid the many dependencies installation in the system. This is why in this appart I will share my knowledge to configure this. Flatpak is a framework for distributing desktop applications across various Linux distributions. It has been created by developers who have a long history of working on the Linux desktop, and is run as an independent open source project.

## Installation 📦

```
sudo apt install flatpak 
sudo gnome-software-plugin-flatpak
```

**Stable Repositories**
```
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak update --appstream
```

**Beta Repositories**
```
flatpak remote-add --user flathub-beta https://flathub.org/beta-repo/flathub-beta.flatpakrepo
flatpak update --appstream
```
If you are having issues with XDG_DATA_DIRS, execute **echo export `XDG_DATA_DIRS="/opt/myapp/share:$XDG_DATA_DIRS"' >> ~/.xsessionrc**

## Permissions 🙅🏻

<p align='center'>
	<img src='https://raw.githubusercontent.com/HBlanqueto/HBlanqueto/master/wayland/flatseal.png'/>
</p>

I recommend **Flatseal**, a program that allows you to edit the permissions of the Flatpak packages that you use, it is very easy and intuitive to use so that you are not doing commands all the time, so if anything you can use both.

```
flatpak install flathub com.github.tchx84.Flatseal
```

## Themes 🎨

If you have problems using dark themes in flatpak, you will most likely need this package which contains Adwaita Dark, it not only works if you use dark themes, but it is also in case your desktop has automatic dark modes.

**Adwaita Dark Theme**
```
flatpak install org.gtk.Gtk3theme.Adwaita-dark
```

**Override System themes in flatpak**

The correct way to override the current GTK theme you use in your system in flatpak. Also you could use `--filesystem=/usr/share/themes` if you install custom themes right there 

```
sudo flatpak override --filesystem=~/.themes
```

## Runtimes 🏃

Runtime describes software/instructions that are executed while your program is running, especially those instructions that you did not write explicitly, but are necessary for the proper execution of your code.

**Freedesktop**
```
flatpak install org.freedesktop.Platform
```

**Gnome Runtimes**
```
flatpak install org.gnome.Platform
```
**KDE Runtimes**

```
flatpak install org.kde.Platform
```