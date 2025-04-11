# Building useful HomeStation from ugly Debian

## Introduction

When the [Debian OS](https://www.debian.org/) was released in 1993, I was in my last year of high school. I enjoyed building programs and employing algorithms, and decided to become a programmer. Today, software development is my profession, but, surprisingly, I had never heard of Debian until 2013.

At that time, I was looking for a good solution for everyday home computing, while at the same time I needed a virtualization station for developing software on Microsoft Windows and Microsoft Visual Studio. There are many variants for virtualization based on Microsoft Windows, for example VMware Virtualization for Desktop or Microsoft Hyper-V, but I can not afford to the time required to adopt Windows 8 or any similar Metro-style interface, nor can I afford to pay each time Microsoft Windows is updated. Moreover, there is an assumption that Microsoft monitoring user activity and collecting private user data. I decided that my desktop computer ought to have free and open software as its primary operating system.

I started my research by considering using Ubuntu 12.04 and Oracle VirtualBox in parallel with Microsoft Windows 8 and Hyper-V. A problem emerged. Despite its impressive appearance, Ubuntu is not always the most stable OS. However, I tied my best to work with it for about 6 months until the arrival of Debian 7 "Wheezy" in May 2013. Debian was quite a contrast to Ubuntu. It was very fast and stable. Unfortunately, it is butt ugly!

It turns out to be quite difficult to make Ubuntu more stable, but fortunately, I figured out how to give Debian a more contemporary appearance, and to work better. Today, Debian 12 "Bookworm" is the primary operating system on my desktop PC.

## Hardware

The stories about compatible hardware for Linux are very funny stories. Probability, the newest hardware will not work on Linux. In addition, ATI or [NVIDIA](http://www.wired.com/2012/06/torvalds-nvidia-linux/) discrete video card can make an issue. I have never had discrete video cards since 2010 and that saves my nerves and of course, saves money. Today, Intel CPU has faster inbound GPU, and usually it is enough for everything. For example, I am using `Intel i5-9400 Processor`. It is not a new CPU, [but I am happy when news about K and HK series comes](https://duckduckgo.com/?q=intel+K+and+HK+bugs+2023). Also, I never used AMD and I do not know how Debian work on AMD hardware, but this question is [very popular](https://duckduckgo.com/?q=Does+Linux+run+better+on+AMD+or+Intel+hardware). Moreover, at least 8 GB (16 GB and more is better) of memory and CPU with [VT-x](https://en.wikipedia.org/wiki/X86_virtualization#Intel_virtualization_.28VT-x.29) or [AMD-V](https://en.wikipedia.org/wiki/X86_virtualization#AMD_virtualization_.28AMD-V.29) technology is required for virtualization. SSD disk can make Debian faster, but will be great if partition for virtual disks is stored on separate HDD.

And it is not surprising that everyone is ~~mining cryptocurrencies~~ developing AI technologies these days. So, NVidia is a must, are not you? In `Debian` you can use open drivers or non-fee. Users choose non-free mostly.

## Software

Debian has at least [three releases](https://www.debian.org/releases/index.html): stable, testing and unstable. Although software in the stable release are old for two or even four years, the stable release of Debian can be a base for building home using desktop PC. In many cases home user does not know exactly what is the version of software that are using and what is the difference between the actual version of software and the previous version. In some cases, when software is ancient in the stable release, the user can install the most recent version of software from testing release of Debian or directly from vendor repository. Even though I prefer the stable release of Debian, I am using vendor repositories or flatpack, especially for software that I need new.

Unlike Microsoft Windows, Debian has several [desktop environments and window managers](https://wiki.debian.org/DesktopEnvironment). I prefer simple, fast and useful desktop. Actually, newest Gnome3 and KDE are not on this way. Gnome3 looks strange and unfortunately, WinKey does not work with VirtualBox. This problem there is also in Ubuntu and all other graphical environments based on Gnome3. KDE is very glossy and eats amount of memory, but people often like it. XFCE and LXDE is quite spartan and point for slow or old computers. I prefer middle may, therefore I am used to working with [MATE Desktop Environment](http://mate-desktop.com/). The MATE Desktop Environment has evolved from Gnome2 and offers such a great desktop environment. It is really simple, really fast and really useful... Great speech 10 years ago. Currently, KDE is the only competitor.

Default installation of Debian includes a lot of extra software. We will think out of the box and are starting from minimal Debian installation without desktop environment. I prefer a hands-off way to install all necessary software, because it gives me the possibility to install the minimum of software. To do it, when installation of Debian comes to finish, the most important step is on "Software selection" (all items should be deselected):

![Image 1](https://www.codeproject.com/KB/install/1086376/Debian_Software.png)

After the minimal Debian system was installed we can set up our system and will install and will configure desktop environment and user interface.

For more information how to install Debian see the [step by step instruction](https://debian-handbook.info/browse/stable/sect.installation-steps.html).

## Setting up Debian after minimal installation

