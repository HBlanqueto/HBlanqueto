CUPS (formerly an acronym for Common UNIX Printing System) is a modular printing system for Unix-like computer operating systems which allows a computer to act as a print server.

## Dependencies ℹ️

```
sudo apt install cups system-config-printer printer-driver-cups-pdf
sudo systemctl enable cups.service --now
```

## Drivers 🖨 

For this is necessary to investigate about your printe model, in this case I use an Epson L575 so for this kind of printers you have to:

**All Printer Driver**
```
sudo apt install printer-driver-all
```

**Epson**
```
sudo apt install printer-driver-escpr
```