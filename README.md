### Ubuntu Mainline Kernel Installer

This is a tool for installing the latest mainline Linux kernel on Ubuntu-based distributions.

![Main window screenshot](main_window.png)

### Features

* Fetches list of available kernels from [Ubuntu Mainline PPA](http://kernel.ubuntu.com/~kernel-ppa/mainline/)
* Optionally watches and displays notifications when a new kernel update is available
* Downloads and installs packages automatically
* Display available and installed kernels conveniently
* Install/remove kernels from gui
* For each kernel, the related packages (headers & modules) are installed or removed at the same time

### Downloads & Source Code
mainline is written using Vala and GTK3. Source code and binaries are available from the [GitHub project page](https://github.com/aljex/mainline).

### Build
		sudo apt install libgee-0.8-dev libjson-glib-dev libvte-2.91-dev valac
		git clone https://github.com/aljex/mainline.git
		cd mainline
		make
		sudo make install

### About
mainline is a fork of [ukuu](https://github.com/teejee2008/ukuu)

The original author stopped maintaining the original GPL version of ukuu and switched to a [paid license](https://teejeetech.in/tag/ukuu/) for future versions.

### Enhancements / Deviations from the original author's final GPL version

* (from [stevenpowerd](https://github.com/stevenpowered/ukuu)) Options controlling the internet connection check
* (from [cloyce](https://github.com/cloyce/ukuu)) Option to include or hide pre-release kernels
* Changed name from "ukuu" to "mainline"
* Removed all GRUB options
* Removed all donate buttons, links, dialogs
* Remove source cruft

### Development Plans / TODO
* More efficient downloading & caching of info about available kernels  
Stop consuming over 5GB with kernel packages in ```~/.cache/```  
Until then, as a work-around, ```mainline --clean-cache``` deletes the cache
* Better (more automatic) initial sizes for the window and the columns in the kernel list display so you don't have to manually expand them  
...or at least, remember the sizes the user last set.
* Clean up build warnings
* Clean up run-time GTK warnings
* Make http client configurable (curl/wget/other)  
Currently uses aria2c.  
Maybe just by moving the aria2c actions into an external script in ~/.config, where the user could do anything they want, rsync, bittorrent, dummy/fake.
* Reduce dependencies,  
Do we really need aptitude?  
libsoup or other library instead of shell commands for downloads?  
* Customizable appearance, at least colors
* Option to specify kernel variant (generic, lowlatency, snapdragon, etc...)
* Configurable lowest version threshhold instead of the current hard-coded 4.0  
...or, automatically subtract 1 from whatever the current highest release version is
* Improve the annoying pkexec behavior.  
It would be nicer to run pkexec (or lxqt-sudo, etc) one time for the whole session, and only have to enter a password once, instead of once per action.  
But currently, if you actually do that, it creates files in the users home directory that are owned by root, so don't do that.  
This might be addressed by getting the policy kit file working.
* Write a man page
* Make all the terminal & child processes more robust.  
It's always really been pretty 9/10ths-baked.  
Kernel downloads fail, but work if you just do it again.  
dpkg installs fail, but work if you just do it again.  
Populating the main window fails, but works if you just do it again.  
Determining what is currently installed & running fails, but works if you just do it again  
...that is really kind of inexcusable crap and could all be a lot better.
* More careful temp file / temp working dir management.  
It does avoidable dumb things like creating dirs/files as one user and then can't remove or use them later as another user.
* Maybe replace the entire thing with a bash script, maybe with zenity for an optional gui?  
https://github.com/pimlie/ubuntu-mainline-kernel.sh
