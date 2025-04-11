Building useful HomeStation from ugly Debian
============================================

And at the end, `logrotate` package can be removed from Debian. This package allows automatic rotation, compression and mailing of log files but on a desktop it is not necessary. Command for remove `logrotate` package is:

Swap partition can be everywhere. Debian can keep swap data in partitions or in files or works without swap, but swap partition is necessary for hibernate or virtualization. In some cases using SSD disk for swap is not a good solution. In this cases you are the BOSS, but anyway I recommend to reduce swap usage. Reducing swap usage can be setting in `/etc/sysctl.conf` file:

This value (10 in example) should be in percentage of RAM. It means that swap partition will be used in Debian only when there are less than 10% of free RAM.

By default installation, Debian makes a short pause for 5 seconds before starting. Is this a good idea? I think for home users are not. Also, it will be great, if `IP6 protocol` will be disabled during Debian is loading, because running with IP6 can arise problems relating to tunnelling, performance and security. To make it, change `TIMEOUT` value to 0 and add `ipv6.disable=1` to `GRUB_CMDLINE_LINUX_DEFAULT` in `/etc/default/grub` file:

Next time, Debian will start without pause. You may reboot Debian now by following command:

The Debian works with many international keyboards and languages. There are two commands for setup keyboard and console configuration:

These commands update `/etc/default/keyboard` and `/etc/default/console-setup` files. It is enough to work in a single language environment, but when user wants to work with different languages is not enough.

Fortunately, setup of multilingual input for Debian is simple. Keyboard model (`XKBMODEL` option) and language layouts (`XKBLAYOUT` option) are stored in `/etc/default/keyboard` file. Multiple layouts may be specified in a comma-separated list, for example (keyboard with MS Windows keys, American English and Russian language layouts):

Also, `XKBOPTIONS` option contains some extra parameters. For example, `grp:alt_shift_toggle` means that `Alt+Shift` shortcut will be used for switching between language layouts. Another great option is `numpad:microsoft`. It means that `Shift+NumpadKeys` behaviour will be like in Microsoft Windows. As a result, the `/etc/default/keyboard` file will look like that:

In additional, switching between language layouts can be lighted by [status lights on keyboard](https://en.wikipedia.org/wiki/Scroll_lock). Option `grp_led:scroll` in `XKBOPTIONS` means that `Scroll lock` status light will be turned on after language layout was changed.

The Debian repository is a set of available software that can be installed on Debian from CDs, DVDs, local network or Internet. Debian keeps information about repositories in `/etc/apt/sources.list` file. Even though there are a lot of [Debian worldwide mirror sites](https://www.debian.org/mirror/list), I advise to use Debian repository without country specified. Also, default installation Debian uses only `main` components that consists only of [DFSG-compliant packages](https://www.debian.org/social_contract#guidelines). It is good for most of business, but home users may use `contrib` and `non-free` components. Moreover, some of vendor repository can be added in `/etc/apt/sources.list` file for using newest version of software. Next command will open the `/etc/apt/sources.list` file for editing:

By default Debian installation the `/etc/apt/sources.list` file will be similar to:

The first thing we do, let's add the `contrib` components after `main` components in all Debian repositories (excluding original Debian CDs and DVDs). Also, `non-free` components can be added, if you are not afraid of using the non free software.

At final, we can comment all `deb-src` Debian repositories with symbol `#`, because these repositories is not really needed for home users. After all changes, the `/etc/apt/sources.list` file will looks like that:

Now, Debian list of available packages can be updated by command:

sudo apt-get update

The following command will upgrade all installed packages to newer version:

sudo apt-get upgrade

More information about repositories in Debian: [https://wiki.debian.org/SourcesList](https://wiki.debian.org/SourcesList)

### 7\. Installing ALSA

There are several types of sound systems that run on Linux. Main of them are `ALSA` and `PulseAudio`. PulseAudio serves as a proxy to sound applications using existing kernel sound components, but PulseAudio does not work correct in many cases on Debian. Therefore, PulseAudio is not necessary and I prefer ALSA. For installing ALSA from Debian repository run the command:

sudo apt-get install alsa-base alsa-utils

After ALSA was installed sound card should be initialized by command:

sudo alsactl init

Command `aplay` can be a standard test for speakers:

aplay /usr/share/sounds/alsa/\*

More information about Advanced Linux Sound Architecture in Debian: [https://wiki.debian.org/ALSA](https://wiki.debian.org/ALSA)

### 8\. Installing X Window System

Before installing MATE Desktop Environment, the [X Window System](https://en.wikipedia.org/wiki/X_Window_System) should be installed and configured. The X Window System (or X11) draws and moves windows on the display and interacts with a mouse and keyboard. Installation of X Window System can be done by command:

sudo apt-get install xorg

Be careful, because installation of `X Window System` contains approximately 140Mb-150Mb and most of packages can be taken from Debian DVD instead of downloading them from Internet. After the `X Window System` has installed, the font visualization should be configured by following command:

sudo dpkg-reconfigure fontconfig-config

To improve Debian looks should be selected following answers: `Autohinter`, `Always` and `No` (this step is very important, especially for LCD monitors):

![Image 6](https://www.codeproject.com/KB/install/1086376/Debian_FontConfig_1.png)

![Image 7](https://www.codeproject.com/KB/install/1086376/Debian_FontConfig_2.png)

![Image 8](https://www.codeproject.com/KB/install/1086376/Debian_FontConfig_3.png)

More information about fonts file in Debian: [https://wiki.debian.org/Fonts](https://wiki.debian.org/Fonts).

### 9\. Installing MATE

Now we are ready to install the `MATE Desktop Environment`. The `mate-core` package installs minimal MATE Desktop Environment. MATE uses the `PulseAudio` by default. To prevent it, additional two packages should be installed together with `mate-core` package. These packages are `mate-media-gstreamer` and `mate-settings-daemon-gstreamer`:

sudo apt-get install mate-core mate-media-gstreamer mate-settings-daemon-gstreamer

At least 550Mb of software will be installed. Please remember that Debian DVD contains most of them.

The `MATE Desktop Environment` in minimal installation is not useful. Installation of these packages adds more functionality:

`mate-utils` - the tools bundled as MATE utilities  
`mate-system-tools` - a set of administration tools  
`mate-system-monitor` - system monitor allows to view and manipulate the running processes  
`mate-notification-daemon` - displays passive pop-up notifications  
`mate-power-manager` - a power manager  
`mate-screensaver` - screen saver and locker  
`mozo` - an menu editor for MATE that can add and edit new entries and menus  
`caja-open-terminal` - caja extensions which allows to open a terminal  
`caja-gksu` - caja extensions which allows to open files with administration privileges  
`qt4-qtconfig` - configuration program allows to configure the look and behaviour of any Qt4 application  
`cpufrequtils` - two utilities for inspecting and setting the CPU frequency  
`ntp` - Internet clock synchronization  
`synaptic` - a graphical package management tool

The command to install is:

sudo apt-get install mate-utils mate-system-tools mate-system-monitor mate-notification-daemon mate-power-manager mate-screensaver mozo caja-open-terminal caja-gksu qt4-qtconfig cpufrequtils ntp synaptic

These packages are necessary to improve the appearance:

`clearlooks-phenix-theme` - a GTK2 and GTK3 themes which is a port of Clearlooks  
`chameleon-cursor-theme` - different mouse themes with colours  
`mate-icon-theme-faenza` - the Faenza icon theme provided with the MATE desktop  
`ttf-mscorefonts-installer` - Microsoft fonts improve LibreOffice, web surfing and compatibility

The command to install is:

sudo apt-get install clearlooks-phenix-theme chameleon-cursor-theme mate-icon-theme-faenza ttf-mscorefonts-installer

After the `chameleon-cursor-theme` package has installed, the system mouse cursor can be chosen by following command:

sudo update-alternatives --config x-cursor-theme

I prefer the `Chameleon-SkyBlue-Regular`, but you are free to choose yours theme.

The `GStreamer` plugins are necessary for listen to music and watching media. Most important `GStreamer` plugins (`gstreamer0.10-plugins-base`, `gstreamer1.0-plugins-base`, `gstreamer0.10-plugins-good` and `gstreamer1.0-plugins-good`) were probability installed. Also, set of `bad` and `ugly` plugins can be installed. Installation coomand is:

sudo apt-get install gstreamer0.10-plugins-bad gstreamer0.10-plugins-ugly gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly

These packages is not necessary and depends by user favourites:

`wicd` - a system network service that manages network devices and connections, can be replaced by [network-manager-gnome](https://wiki.gnome.org/Projects/NetworkManager) or by each other preferred network manager  
`galculator` - calculator  
`eom` - is a simple graphics viewer for the MATE desktop  
`atril` - a simple multi-page document viewer  
`mousepad` - a graphical text editor for Xfce, but is so a good for MATE also, can be replaced by each other preferred text editor, for example `pluma` or `geany`  
`gimp` - an advanced picture editor  
`engrampa` - an archive manager for the MATE environment  
`transmission-gtk` - lightweight BitTorrent clients  
`gmusicbrowser` - a lightweight media player, mostly used for play audio files and songs, can be replaced by each other preferred audio player, but remember that `ALSA` was installed instead of PulseAudio  
`soundconverter` - a simple sound converter application, especially for preparing songs for different mobile devices, it is not strictly necessary  
`easytag` - an utility for viewing, editing and writing the tags of different audio files, it is not strictly necessary  
`smplayer` - simple video player, can be replaced by `vlc` or by each other video player  
`brasero` - a simple application to burn, copy and erase CD and DVD media, it is not strictly necessary

The command to install is:

sudo apt-get install wicd galculator eom atril mousepad gimp engrampa transmission-gtk gmusicbrowser smplayer soundconverter easytag brasero

Also, there is the `apt-xapian-index` package - a tool to maintain Debian package information and allows the `synaptic` using a quick search panel. Usually this package is not necessary because it makes so many writing to SSD and Installation command is:

sudo apt-get install apt-xapian-index

#### Internet browser

[`Iceweasel`](https://wiki.debian.org/Iceweasel) is the default Internet browser in Debian that is re-branded `Firefox` for Debian. Next command will install `Iceweasel`:

sudo apt-get install iceweasel

The default browser can be replaced by native `Firefox`, `Chromium` or each [other preferred Internet browser](https://wiki.debian.org/WebBrowsers). The Debian Mozilla team provides related packages for use on Debian systems and I prefer native `Firefox`. To install this browser from vendor repository, the archive key of Debian Mozilla team repository should be added to the Debian list of trusted keys by following command:

wget -q http://mozilla.debian.net/archive.asc -O- | sudo apt-key add -

Second step, Debian Mozilla team repository should be added to the `/etc/apt/sources.list` file (see above) by following line:

deb http://mozilla.debian.net/ jessie-backports firefox-release

After that, the native `Firefox` can be installed by command:

sudo apt-get update
sudo apt-get install firefox

Instead of `Firefox`, the [`Chromium browser`](http://www.chromium.org/) is the open source project behind Google Chrome and this browser can be installed by following command:

sudo apt-get install chromium chromium-l10n

If the [`Opera browser`](http://www.opera.com/) is prefered, then instruction for installing can be found here: [https://wiki.debian.org/Opera](https://wiki.debian.org/Opera)

In addition, the [Adobe Flash](https://en.wikipedia.org/wiki/Adobe_Flash) is situated in the flashplugin-nonfree package that is from the nonfree components of Debian repository. It can be installed by command:

sudo apt-get install flashplugin-nonfree

The Adobe Flash is often released and can be updated in Debian by command:

sudo update-flashplugin-nonfree --install

#### LibreOffice and language tools

Home users need at least a [word processor](https://en.wikipedia.org/wiki/Word_processor) and a [spreadsheet program](https://en.wikipedia.org/wiki/Spreadsheet). The LibreOffice has all of them:

`libreoffice-writer` - a word processing and desktop publishing tool  
`libreoffice-calc` - a spreadsheet program  
`libreoffice-gtk` - plugin for drawing LibreOffices widgets  
`libreoffice-style-sifr` - an adaption of the Gnome symbolic theme, nice and pretty looks

sudo apt-get install --no-install-recommends libreoffice-writer libreoffice-calc libreoffice-gtk libreoffice-style-sifr

Also, if you are interested in presentations and databases, then following packages can help you:

`libreoffice-base` - full-featured desktop database front end  
`libreoffice-impress` - tool for creating multimedia presentations

sudo apt-get install libreoffice-base libreoffice-impress

Next command will install all LibreOffice packages and a little more:

sudo apt-get install libreoffice

Debian has a lot of language tools. Remember, language tools, thesaurus, and dictionaries may are used by different Debian software, for example LibreOffice and Firefox use it to check spelling. You must want to install all languages that you can write.

`hyphen-en-us` - contains the English (USA) hyphenation patterns, also additional patterns can be installed by user preferences (for example `hyphen-fr`)  
`hunspell-en-us` - American English dictionary for `hunspell` spellchecker, also additional dictionaries can be installed by user preferences (for example `hunspell-en-ca`)  
`aspell-en` - support for English language to the `GNU Aspell` spell checker, also additional languages can be installed by user preferences (for example `aspell-fr`)  
`mythes-en-us` - contains an English thesaurus, also additional thesauruses can be installed by user preferences (for example `aspell-fr`)

Following example may be helpful for users who live in Canada and writing Russian ([American English](https://en.wikipedia.org/wiki/American_English), [Canadian English](https://en.wikipedia.org/wiki/Canadian_English) and [Russian](https://en.wikipedia.org/wiki/Russian_language) language tools):

sudo apt-get install hyphen-en-us hyphen-ru hunspell-en-us hunspell-en-ca hunspell-ru aspell-en aspell-ru mythes-en-us mythes-ru

#### Oracle VirtualBox

I believe that `Oracle VirtualBox` is the best virtualization solution for home users on Debian. Unfortunately, Debian repository contains the very oldest version of VirtualBox. If you are interested in newest version of VirtualBox, then add next two archive keys to the Debian list of trusted keys by commands:

wget -q https://www.virtualbox.org/download/oracle\_vbox\_2016.asc -O- --no-check-certificate | sudo apt-key add -

wget -q https://www.virtualbox.org/download/oracle\_vbox.asc -O- --no-check-certificate | sudo apt-key add -

After that, add the Oracle repository to the `/etc/apt/sources.list` file:

deb http://download.virtualbox.org/virtualbox/debian jessie contrib

If Oracle repository was added to `/etc/apt/sources.list` file (see above the step number 6) then newest `Oracle VirtualBox` version 5.1 can be installed by command (be aware, version 5.1 uses Qt5 libraries):

sudo apt-get install virtualbox-5.1

Alternatively, you can install VirtualBox 5.0 which do not use Qt5 libraries.To install Oracle VirtualBox version 5.0 use command:

sudo apt-get install virtualbox-5.0

To install Oracle VirtualBox from Debian repository (version 4.3.18):

sudo apt-get install virtualbox-qt

#### Installing a display manager

The `X Window System` should have a display manager. It is a graphical login manager which presents a login screen and starts a session after an user enters a valid combination of username and password. I prefer the [SLiM](https://en.wikipedia.org/wiki/SLiM), because it aims to be light and completely configurable, but the [LightDM](https://wiki.debian.org/LightDM) is good also and has more functionality. Anyway, display manager is only for starting `X Window System` and run a desktop environment. Therefore, extended functionality is not necessary in this step. To install `SLiM` display manager use the following command:

sudo apt-get install slim

The `SLiM` display manager can be configured to prevent log and automatically starts user session (auto login) in `/etc/slim.conf` file. Next command will open `/etc/slim.conf` file for editing:

sudo nano /etc/slim.conf

Necessary changes can be done in following sections:

default\_user    **yes**
logfile         ^\_\_b class="highlight">/dev/null

To install the `LightDM` display manager (if you are prefer it instead of `SLiM`) use the following command:

sudo apt-get install --no-install-recommends lightdm

The `LightDM` recommends installing a lot of packages that usually are not necessary. The configuration file for `LightDM` display manager is `/etc/lightdm/lightdm.conf` and this file can be edit by command:

sudo nano /etc/lightdm/lightdm.conf

Automatically starts user session can be configured in `[SeatDefaults]` section:

\[SeatDefaults\]
...
autologin-user=
**autologin-user-timeout=^\_\_b class="highlight">0**

Now we can reboot our PC by command:

sudo reboot

After that instead of console we will start working with MATE Desktop Environment, but Debian continues to be uncomfortable:

![Image 9](https://www.codeproject.com/KB/install/1086376/Debian_MATE.png)

### 10\. Setting up MATE

Time to make Debian beautiful and useful and we have installed all packages for it.

#### Fontconfig

`Fontconfig` uses XML format for its configuration files. User preferences should be setting up in `~/.fonts.conf` file that is places in each user home folder. This is a link file, real data are stored in `/home/<username>/.config/fontconfig/fonts.conf` file. Debian provides link file for back compatibility. Bellow is an example of my `~/.fonts.conf` file:

nano ~/.fonts.conf

\="1.0"
<!DOCTYPE fontconfig SYSTEM "fonts.dtd"\>
<fontconfig\>
 <match target\="font"\>
  <edit mode\="assign" name\="hinting"\>
   <bool\>true</bool\>
  </edit\>
 </match\>
 <match target\="font"\>
  <edit mode\="assign" name\="hintstyle"\>
   <const\>hintslight</const\>
  </edit\>
 </match\>
 <match target\="font"\>
  <edit mode\="assign" name\="rgba"\>
   <const\>rgb</const\>
  </edit\>
 </match\>
 <match target\="font"\>
  <edit mode\="assign" name\="antialias"\>
   <bool\>true</bool\>
  </edit\>
 </match\>
 <match target\="font"\>
   <edit mode\="assign" name\="lcdfilter"\>
   <const\>lcddefault</const\>
   </edit\>
 </match\>
</fontconfig\>

Same practices should be done for `~/.Xdefaults` file in each user home folder. Bellow is an example of my `~/.Xdefaults` file:

nano ~/.Xdefaults

Xft.autohint: 0
Xft.lcdfilter: lcddefault
Xft.hintstyle: hintslight
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

After that, run the command for each user:

xrdb -merge ~/.Xdefaults

And at the end, following command will regenerating fonts cache:

sudo dpkg-reconfigure fontconfig

More information about fonts file in Debian: [https://www.freedesktop.org/software/fontconfig/fontconfig-user.html](https://www.freedesktop.org/software/fontconfig/fontconfig-user.html) and [https://en.wikipedia.org/wiki/Fontconfig](https://en.wikipedia.org/wiki/Fontconfig)

#### Appearance preferences

Here are the biggest things that should be done. We will setting up visualization theme. This is a set of rules that MATE will use when windows and controls are drawing on display. These rules can be setup from main MATE menu: `System > Preferences > Appearance`. Select the `Clearlooks-Phenix` theme from the Theme tab. This theme works perfect in GTK 2 and GTK 3 environments, also QT-based applications will look the similar as GTK-based applications:

![Image 10](https://www.codeproject.com/KB/install/1086376/Appearance_1.png)

After that theme was selected, press the `Customize...` button for setting up some details. First, select the `MATE-Faenza` icon theme on the Icons tab:

![Image 11](https://www.codeproject.com/KB/install/1086376/Appearance_3.png)

Second, select favourite mouse cursor theme on the Pointer tab. For example `Chameleon-SkyBlue-Regular`:

![Image 12](https://www.codeproject.com/KB/install/1086376/Appearance_4.png)

After that, back to the `Appearance Preferences` form and setting up fonts on Fonts tab. We installed the `Noto Sans fonts` before. These fonts are so good for user interface:

![Image 13](https://www.codeproject.com/KB/install/1086376/Appearance_5.png)

Moreover, `Smoothing` and `Hinting` can be set after press the `Details...` button. I prefer `Subpixel (LCDs)` and `Slight`, but you are free to decide yours favourites:

![Image 14](https://www.codeproject.com/KB/install/1086376/Appearance_6.png)

And at the end, we will setup Qt Configuration. It can be done from main MATE menu: `System > Preferences > Qt 4 Settings`. You have to select the `GTK+` value from drop-down `GUI Style` list that on Appearance tab:

![Image 15](https://www.codeproject.com/KB/install/1086376/Qt_Configuration.png)

After that, all Qt-based applications will look similar as GTK-based applications, for example Oracle VirtualBox.

#### Preferred Applications

If `gmusicbrowser` or `easytag` was installed, then you have to correct a few problems. First, remove comment symbol from `#MimeType=` line for `gmusicbrowser` in `/usr/share/applications/gmusicbrowser.desktop` file. Next command will open this file for editing in terminal:

sudo nano /usr/share/applications/gmusicbrowser.desktop

...
StartupNotify=true
Comment\[fr\]=Jukebox pour de grandes collections de mp3/ogg/flac/mpc
**#**MimeType=audio/x-musepack;application/x-musepack;audio/musepack;application/mu...

After `/usr/share/applications/gmusicbrowser.desktop` file was changed run following command:

sudo update-desktop-database

Next step can be done from main MATE menu: `System > Preferences > Preferred Applications`. You have to select your favourites, especially on Multimedia and System tabs:

![Image 16](https://www.codeproject.com/KB/install/1086376/Preferred_Applications_1.png)

Be aware, that sometimes `easytag` puts itself in File Manager drop-down list on System tab. Check this problem and change the `easytag` to the `Caja` in the File Manager drop-down list:

![Image 17](https://www.codeproject.com/KB/install/1086376/Preferred_Applications_2.png)

Also, you may want that standard text editor (for example `Mousepad`) should be used instead of LibreOffice Writer. It can be setup in Text Editor drop-down list on System tab.

#### Clock indicator

Set your locations is important, because Debian synchronizes date and time from Internet. Also, Debian shows the weather conditions at your location. Mouse click on the `Clock indicator` on MATE panel will open calendar. Locations can be set up by click on `Edit` button:

![Image 18](https://www.codeproject.com/KB/install/1086376/Clock_Indicator.png)

#### Volume Control Indicator

If you prefer to see the sound icon like in Microsoft Windows, then you should add the `Volume Control Indicator` by right-click on MATE panel.

![Image 19](https://www.codeproject.com/KB/install/1086376/Volume_Indicator.png)

This indicator allows to change volume control by mouse wheel and to mute sound by double click. Also, it provides pop-up sound control panel by left-click.

#### LibreOffice User Interface

LibreOffice User Interface can be set up from menu of anything LibreOffice program: `Tools > Options > View`. We have installed `libreoffice-style-sifr` package before. This package provides greyed style and can be selected in `Icon size and style` drop-down list.

![Image 20](https://www.codeproject.com/KB/install/1086376/OpenOffice_Style.png)

After `Sifr` style has selected, LibreOffice will look a little more elegant:

![Image 21](https://www.codeproject.com/KB/install/1086376/OpenOffice_View.png)

#### MATE panel

Many users find that dual panels is convenient. But there are users who prefer Microsoft Windows layout with a single panel. To make MATE with a single panel, existing bottom panel should be deleted and orientation of top panel should be `Bottom` in the `Properties` menu. And at the end, add `Windows List` to the MATE panel.

![Image 22](https://www.codeproject.com/KB/install/1086376/MATE_Panel.png)

#### Keyboard indicator

To show the keyboard flag in the taskbar run command in MATE:

gsettings set org.mate.peripherals-keyboard-xkb.indicator show-flags true

Flag icons can be stored in `/usr/share/icons/flags` folder. If this folder does not exist, run following command for creating it:

sudo mkdir /usr/share/icons/flags

Lubuntu has such the pretty nice flag icons. You can get these flag icons from [Lubuntu Live DVD](https://help.ubuntu.com/community/Lubuntu/GetLubuntu) or download they from archive: [https://pkgs.org/download/lubuntu-lxpanel-icons](https://pkgs.org/download/lubuntu-lxpanel-icons). In both cases, the icons should be copied from `/usr/share/lxpanel/images/xkb-flags-cust/` folder in Lubuntu live CD or archive to the `/usr/share/icons/flags/` folder in your desktop. For example:

![Image 23](https://www.codeproject.com/KB/install/1086376/kbi.png)

#### Ubuntu fonts and Mint icons

I would like to propose the fonts from [Ubuntu](http://font.ubuntu.com/) and the icons from [Mint](https://github.com/linuxmint/mint-x-icons). These things is much better than default fonts and icons in Debian. But be aware, that the `Ubuntu-M.ttf` and `Ubuntu-MI.ttf` fonts are not working in the Debian, therefore do not install it. These fonts can destruct the view of KDE applications.

Now, the Debian 8 will "shine bright like a diamond in the sky"...

### Credits

I would like to thank Mr. Ralph Neelands, my LINC Teacher who advised and helped me to revise this article.
