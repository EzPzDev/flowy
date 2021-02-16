<img src="https://raw.githubusercontent.com/vineetred/nGram/vineetred-patch-1/isolated-monochrome-black.svg" width="20%"> </img>

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0) ![crates.io](https://img.shields.io/crates/v/flowy.svg) ![CI](https://github.com/vineetred/flowy/workflows/CI/badge.svg?branch=master)


## Demo
<p align="center">
  <img src="https://github.com/vineetred/flowy/blob/master/demo/demo2.gif?raw=true" alt="Flowy demo"/>
</p>

<p align="center">
  <img src="https://github.com/vineetred/flowy/blob/master/demo/demo.gif?raw=true" alt="Flowy demo"/>
</p>

## Usage
* The documentation can be found at https://docs.rs/flowy.
* You can either download the binary or get the Debian package.
* Flowy comes with a preset ```lake``` set of wallpapers. See the binary section for more information.
* Flowy can also change the wallpapers based on **sunrise** and **sunset** timings of your location. See the Solar section for more information.

### Binary
* It can be either found in the Releases section or can be installed using Cargo by running the command ```cargo install flowy```.
* If you use the binary, just run it by typing ```flowy -d``` or ```flowy --dir \path\to\wallpapers``` to set the path to the wallpaper directory.
* In case you want to use the preset wallpapers, run ```flowy --preset lake``` or ```flowy -p lake```. This downloads the Lakeside wallpapers made by Louis Coyle. They can also be found [here](https://bucket-more.s3.ap-south-1.amazonaws.com/uploads/lake.tar.gz).
* If you're using Linux, you can let the binary run forever in a terminal session or setup a ```systemd``` service so it listens in the background. Checkout the 'Systemd Automation' section for more details.

### Systemd Automation (Linux only)
* Instead of letting flowy run in an open terminal, it can be run as a background service.
* Create a file called ```flowy.service``` and place it in ```/etc/systemd/user```
* Populate this file with the following contents - 
```
[Unit]
Description=flowy

[Service]
Environment=XDG_CURRENT_DESKTOP=<value>
ExecStart=<command>

[Install]
WantedBy=multi-user.target
```
* Here, replace the variable ```<value>``` with the value of your current Desktop Environment and replace the variable ```<command>``` with whatever mode you would flowy to run in (you should ignore the phrase ```flowy``` while setting the variable ```<command>```).
* Your current Desktop Environment can be found by running the command ```echo $XDG_CURRENT_DESKTOP```.
* After this, one can just run flowy by running the command ```systemctl --user start flowy.service```.
* You can track flowy's status using the command ```systemctl --user status flowy.service```.

### Debian Package
* This release has been deprecated.
<!-- ### Debian package
* If you use the Debian package, then it will install flowy as a ```systemd``` service. During installation, flowy will ask you your directory.
* Once the installation is done, run the command ```systemctl --user start flowy.service``` to run the application.
* Once installation is done and you would still like to change the directory, go to the systemd service file found at ```/etc/systemd/user``` and change the directory in that file. -->

## Wallpapers directory
* The wallpapers inside the directory must be named sequentially.
* For example, if you have 11 wallpapers, the names must be ```paper-01.jpg, paper-02.jpg...```.
* It does not matter what the names of the files are as long as they are sequential.
* Ensure that no matter which OS you are running flowy on, stick to quoted UNIX notation when providing the directory.

## Solar - Sunrise and Sunset
* Flowy can take into account your location's sunrise and sunset timings.
* This option can be used by running ```flowy --solar /path/to/dir lat lon``` and passing flowy the path to the wallpapers, latitiude, and longitude of your location.
* Keep in mind that the wallpapers in the path must be segregated by adding ```DAY``` or ```NIGHT``` tags within the wallpaper names. This is done so that flowy knows which wallpapers to show during the day and which wallpapers to show during the night. The normal sequential numbering rules mentioned in the ```Wallpapers directory``` subsections still apply.
* Example naming scheme - ```DAY-01.jpg, DAY-02.jpg, NIGHT-03.jpg, NIGHT-04.jpg,...```.
* If you do not want to segregate, use flowy in the normal mode (```--dir```).
  
## Experimental
* By default, flowy evenly sets the wallpaper change time based on the number of wallpapers there are. In case you would like to modify these times, it can be done so by editing the ```config.toml``` file found in the config directory. You need to comment the ```flowy::generate_config``` function call in ```main.rs``` and then build it after modifying the config file.

  The location of the config directory depends on your operating system:
  * `~/.config/flowy` on Linux
  * `C:\User\Alice\AppData\Roaming\flowy` on Windows (Windows is not supported ATM)
  * `/Users/Alice/Library/Preferences/flowy` on macOS

## Supported Environments
* **macOS** - Apple Silicon and Intel based chips
* **GNOME Based** - Ubuntu, Fedora, Pantheon
* Linux Mint Cinnamon
* Linux Mint MATE
* Deepin
* XFCE
* KDE
* BSPWM and i3 (with feh)
* **Windows** 7/8/10

**TODO**
* GUI
* Match the stars given the location
* Add support for other platforms, both UNIX and Windows.
* Refactor OS related code to another file
