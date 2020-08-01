# MediaServer Notes

## Introduction
In July, 2020, I used an old laptop with a busted screen to setup as a Linux media server to download and stream movies and TV episodes over my LAN to various wifi devices (laptops, tablets and smart TVs). Below are the notes of the various steps taken and software installed in order to achieve this.

The hardware specs of my old laptop are given below:
  1. Laptop Model: [SAMSUNG model: NP300E5X-U01IN](https://www.samsung.com/in/support/model/NP300E5X-U01IN/)
  
  2. Output if [inxi -F](https://smxi.org/docs/inxi.htm):
  
  ```console
    admin@MediaServer:~$ inxi -F
    System:    Host: MediaServer Kernel: 5.4.0-42-generic x86_64 bits: 64 Console: tty 0 Distro: Ubuntu 18.04.4 LTS
    Machine:   Device: laptop System: SAMSUNG product: 300E4C/300E5C/300E7C v: 0.1 serial: N/A
               Mobo: SAMSUNG model: NP300E5X-U01IN v: FAB1 serial: N/A
               UEFI [Legacy]: Phoenix v: P06RAC date: 10/25/2012
    Battery    BAT1: charge: 47.5 Wh 100.0% condition: 47.5/47.5 Wh (100%)
    CPU:       Dual core Intel Core i3-2310M (-MT-MCP-) cache: 3072 KB
               clock speeds: max: 2100 MHz 1: 843 MHz 2: 822 MHz 3: 844 MHz 4: 805 MHz
    Graphics:  Card-1: Intel 2nd Generation Core Processor Family Integrated Graphics Controller
               Card-2: NVIDIA GF108M [GeForce GT 620M]
               Display Server: X.org 1.20.8 drivers: i915,nvidia tty size: 192x49 Advanced Data: N/A out of X
    Audio:     Card-1 NVIDIA GF108 High Definition Audio Controller driver: snd_hda_intel
               Card-2 Intel 7 Series/C216 Family High Definition Audio Controller driver: snd_hda_intel
               Sound: Advanced Linux Sound Architecture v: k5.4.0-42-generic
    Network:   Card-1: Qualcomm Atheros AR9485 Wireless Network Adapter driver: ath9k
               IF: wlp2s0 state: up mac: 50:b7:c3:b2:80:88
               Card-2: Realtek RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller driver: r8169
               IF: enp3s0 state: down mac: 50:b7:c3:7e:36:ef
    Drives:    HDD Total Size: 500.1GB (56.0% used)
               ID-1: /dev/sda model: ST500LM030 size: 500.1GB
    Partition: ID-1: / size: 458G used: 261G (61%) fs: ext4 dev: /dev/sda1
    RAID:      No RAID devices: /proc/mdstat, md_mod kernel module present
    Sensors:   System Temperatures: cpu: 55.0C mobo: N/A
               Fan Speeds (in rpm): cpu: N/A
    Info:      Processes: 155 Uptime: 18:44 Memory: 2323.2/3714.4MB Init: systemd runlevel: 3
               Client: Shell (bash) inxi: 2.3.56 
  ```
  
  3. Content of /etc/issue:
  
  ```console
    admin@MediaServer:~$ cat /etc/issue
                .-.
          .-'``(|||)
       ,`\\ \\    `-`.               88                         88
      /   \\ '``-.   `              88                         88
    .-.  ,       `___:    88   88  88,888,  88   88  ,88888, 88888  88   88
   (:::) :        ___     88   88  88   88  88   88  88   88  88    88   88
    `-`  `       ,   :    88   88  88   88  88   88  88   88  88    88   88
      \\   / ,..-`   ,     88   88  88   88  88   88  88   88  88    88   88
       `./ /    .-.`      '88888'  '88888'  '88888'  88   88  '8888 '88888'
          `-..-(   )
                `-`

  Welcome to \n \l

  * Services :      Point any Web-Browser to http://\4{wlp2s0} for details
  * DVD Ripping :   Insert the disk in the drive and it should be ripped automatically to the Jellyfish userspace
  * USB Drives :    USB drives are automatically detected and mounted
 ```
 
 4. Content of custom message during remote login by ssh
 
 ```console
    admin@MediaServer:~$ cat /etc/update-motd.d/01-mediaserver-info 
    #!/bin/bash
    #
    #    01-mediaserver-info - print some info about the mediaserver
    #
    #    Authors: Analabha Roy <daneel@utexas.edu>
    #
    #    This program is free software; you can redistribute it and/or modify
    #    it under the terms of the GNU General Public License as published by
    #    the Free Software Foundation; either version 2 of the License, or
    #    (at your option) any later version.
    #
    #    This program is distributed in the hope that it will be useful,
    #    but WITHOUT ANY WARRANTY; without even the implied warranty of
    #    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    #    GNU General Public License for more details.
    #
    #    You should have received a copy of the GNU General Public License along
    #    with this program; if not, write to the Free Software Foundation, Inc.,
    #    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.


    IP_ADDRESS=`/sbin/ifconfig  | grep 'inet '| grep -v '127.0.0.1'|awk '{print $2}'`

    printf "\n"
    printf " * Services :      Point any Web-Browser to http://"$IP_ADDRESS" for details\n"
    printf " * DVD Ripping :   Insert the disk in the drive and it should be ripped automatically to the Jellyfin userspace\n"
    printf " * USB Drives :    USB drives are automatically detected and mounted\n"
```


The key functions required of my home media server are as follows:

  1. That it have a [DLNA](https://windowsreport.com/dlna-servers/) and web-based streaming service for hosting downloaded content on the LAN
  
  2. That it have web based interface to indexer software that searches bittorrent indexes online for content, then download it automatically,
  
  3. That it have a bittorrent client running that has a web based frontend for the benefit of the indexers,
  
  4. That it have a web-based tool to configure and monitor all of the above, 
  
  5. That it have a basic SSH setup, 
  
  6. That it use [hardware transcoding](https://www.streamingmedia.com/Articles/Editorial/Featured-Articles/Hardware-Based-Transcoding-Solutions-Roundup-Testing-Performance-134039.aspx) of audio and video using the onboard NVIDIA graphics card,
  
  7. That it automatically mounts any USB storage devices attached to it (for manually copying content), and
  
  8. That it [automatically rip any DVD](https://www.toptenreviews.com/what-is-the-difference-between-dvd-ripping-and-copying) placed in the DVD drive and allow the content to be streamed.


To these ends, I stripped down my Ubuntu installation from standard to barebones, so that it can run headless without starting X. Then reinstall the nvidia graphics drivers with X so that they're running at least, then setup ssh and remote-login, then setup all the abovementioned software. Note that the servers are not natted to WAN for security reasons.

## Step 1: Make Ubuntu headless

Follow the instructions in the link below:

[Turn Ubuntu desktop into an headless server](https://ubuntuusertips.wordpress.com/2014/02/19/turn-ubuntu-desktop-into-an-headless-server/)

Then, maintain the internet connection, then auto-install the nVidia graphics drivers from the command line as per instructions given below

[2 Ways to Install nVidia Driver on Ubuntu 18.04 (GUI & Command Line)](https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04)

Note that the kernel headers corresponding to the RUNNING KERNEL must be installed. This can be done with the command

```console
sudo apt install linux-headers-$(uname -a|awk '{print $3}')
```

Install and setup the SSH server, and setup the '/etc/issue' file and ubuntu custom message for logins as per the introduction section:

See this HOWTO:

[How to Enable SSH on Ubuntu 18.04](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/)

## Step 2: Install a Media Streaming System:
There are several media streaming servers for Linux, the most popular ones (as of 2020), being [Plex](https://www.plex.tv/) and [Emby](https://emby.media/). I tried both of them. However, Plex was beset with networking difficulties, and [disallowed hardware transcoding unless you paid for their premium service](https://support.plex.tv/articles/115002178853-using-hardware-accelerated-streaming/). Furthermore, the free version of Emby did practically nothing, and you had to pay premium for using any client on a smart TV. Thus, I settled for the open source fork of Emby, called [Jellyfin media server](https://jellyfin.org).

Install Jellyfin as per instructions here:

[Jellyfin Quick Start: Installing on Ubuntu](https://jellyfin.org/docs/general/administration/installing.html#ubuntu)

Then enable hardware transcoding with [nVidia NVENC/NVDEC](https://developer.nvidia.com/nvidia-video-codec-sdk) and the version of FFMPEG bundled with Jellyfin. Instructions are below.

[Jellyfin Quick Start: Hardware Acceleration](https://jellyfin.org/docs/general/administration/hardware-acceleration.html)

**Note:** Even without an nVidia card, hardware transcoding is possible in standard Intel graphics cards using the open source [VAAPI](https://www.freedesktop.org/wiki/Software/vaapi/) libraries. For instructions on how to get Jellyfin to do it, see the HOWTO below:

[Jellyfin Quick Start: Hardware Acceleration using VAAPI](https://jellyfin.org/docs/general/administration/hardware-acceleration.html#configuring-vaapi-acceleration-on-debianubuntu-from-deb-packages)

Finally, I opted for RAM transcoding, where transcoded files are written to RAM instead of disk for faster access. For background, checkout the youtube video below (this one is for Plex, but the principle is the same for all streaming servers)

   [![5 Ways to optimize your Plex Media Server](https://img.youtube.com/vi/F_Pc_4SahWg/0.jpg)](https://www.youtube.com/watch?v=F_Pc_4SahWg)
   
 To create a ramdisk and mount it on ubuntu, follow this HOWTO:
 
 [How to Create and Use a Ramdisk on Ubuntu 18.04](https://linuxhint.com/ramdisk_ubuntu_1804/)
 
 I chose to mount it on the path ['/dev/shm'](https://www.cyberciti.biz/files/linux-kernel/Documentation/filesystems/tmpfs.txt), and use the Jellyfin transcode settings page to point the transcoder to it (see screenshot below). The settings can be obtained by navigating in the Jellyfish Home page as follows: Navigation menu on the left + "Admin : Dashboard --> Playback --> Transcoding (top of the page)"
 
  <a href="https://ibb.co/27F6f46"><img src="https://i.ibb.co/Lz0P27P/image.png" alt="image" border="0"></a>

  As can be seen in the screenshot above, the transcoder setting can be used to enable nVidia NEVC transcoding as described in the Jellyfin "Quick Start" page (linked above) on Hardware Acceleration.
  
## Step 3: Install bittorrent client and indexers:

1. Bittorrent client: I've chosen [transmission](https://transmissionbt.com/), but [deluge](https://deluge-torrent.org/) also has a web interface. Installing transmission without a GUI (headless) and running the web interface can be done as per the instructions below:

    [How to set up transmission-daemon on a Raspberry Pi and control it via web interface](https://linuxconfig.org/how-to-set-up-transmission-daemon-on-a-raspberry-pi-and-control-it-via-web-interface). Note that it doesn't have to be done in a raspberry pi. The instructions will work on any computer running Debian or Ubuntu Linux.

2. Bittorrent indexers: For movies, I chose to install [Radarr](https://radarr.video/) and for TV shows, I chose [Sonarr](https://sonarr.tv/). For details on setting them up. check out their GitHub pages:

    a. Radarr: [GitHub Page](https://github.com/Radarr/Radarr)
  
    b. Sonarr: [GitHub Page](https://github.com/Sonarr/Sonarr)
  
   Note that you will have to setup supported online indexers for bittorrent. There are only a few for Radarr and Sonarr, and they don't always work well. Therefore, I also installed the Jackett proxy server which connects to thousands of online indexers and configured radarr and sonarr to use Jackett instead. For instructions, checkout the [GitHub page for jackett](https://github.com/Jackett/Jackett).
 
  For further details, checkout these HOWTOs:
 
   * [How to use Jackett with Sonarr](https://community.seedboxes.cc/articles/how-to-use-jackett-with-sonarr)
  
   * [Sonarr – How to add good Public Indexers](https://tricksty.com/tricks/sonarr-how-to-add-good-public-indexers)
  
   * [Installing Radarr, Sonarr and Deluge on your Unraid Server](https://blog.harveydelaney.com/installing-radarr-sonar-and-deluge-on-your-unraid-setup/)

3. Finally, in order to keep the Transmission client download list from bloating, I used this HOWTO to automatically remove completed downloads from transmission:

    [Guide : Auto removal of downloads from transmission 2.82](https://community.wd.com/t/guide-auto-removal-of-downloads-from-transmission-2-82/93156)

## Step 4: Automounting USB and Automatic DVD-Ripping

Here, I wanted to setup the media server in such as way that inserting a USB thumb drive or external hard drive into the machine would automatically mount it without manual intervention. This way, I can remotely log in and just copy the files from the drives to wherever. The simplest way is to use Ubuntu's systemd to launch the automount service at boot, the service being [automount-usb](https://github.com/raamsri/automount-usb). Simply checkout the github repository and follow the instructions therein

  ```console
  $ git checkout https://github.com/raamsri/automount-usb
  $ cd automount-usb
  $ sudo ./CONFIGURE.sh
  ```
 In addition, I setup the system to automatically mount and rip any inserted DVD discs and copy the content files over to a separate folder in the Jellyfin media user space. To do that, I setup [Automatic Ripping Machine (ARM)](https://b3n.org/automatic-ripping-machine/). Just check out the [relevant GitHub page](https://github.com/automatic-ripping-machine/automatic-ripping-machine) and follow the instructions therein.


## Step 5: Setup unified interface using Organizr and EasyServerMonitor:
Phew! That was a lot of installations and configs! Now, the media server has a lot of web services running in all sorts of ports, with more possibly in the future. How does one keep track of it all? Bookmarks in the browser? UGH! What about checking up on server status? Do we just keep ssh-ing periodically? How crude!

An excellent software for keeping all your media services together for easy viewing and configuration is called ["Organizr"](https://organizr.app/). It sets up a web login using PHP on an standard web server where you can keep all your media service links in one place and see a status dashboard to boot! Head on over to [their documentation](https://docs.organizr.app/) and follow the installation instructions. Alternatively, see the following article (adjust for your operating system)

  [The Ultimate Organizr V2 Setup Guide for Windows](https://smarthomepursuits.com/install-organizr-v2-windows/)

The setup instructions can be a bit confusing, so I summarize below.

  1. First, setup an http web server with php hooks enabled. I chose the lightweight ['lighttpd'](https://www.lighttpd.net/) server due to its speed and small footprint, but more standard ones like [Apache](https://httpd.apache.org/) or [Nginx](https://www.nginx.com/) can also be used. See this HOWTO on setting up lighttpd with PHP enabled:
  
   [Setup Lighttpd Web Server with PHP Supports on Ubuntu Servers](https://websiteforstudents.com/setup-lighttpd-web-server-with-php-supports-on-ubuntu-servers/)

  2. Next, Clone/Download the GitHub page of [OrganizrInstaller](https://github.com/elmerfdz/OrganizrInstaller), navigate to the folder for the ubuntu installer script, and launch it.
     
     ```console
     $ git clone https://github.com/elmerfdz/OrganizrInstaller
     $ cd OrganizrInstaller/ubuntu/oui
     $ sudo bash ./ou_installer.sh
     ```
     
## Step 6: Users, Groups and Permissions

Finally, since all the different softwares installed above often want to communicate content data to each other in disk, I thought it best to let them. To that end, each software creates a user and group with the same name as the software (this is done automatically). Set the working directories of each of the following software to permissions where the user and group gets to read, write and execute, and assign  the groups to each other. Consult standard linux documentation on how to do this. The following users/groups are important in this regard:

1. Group: admin, Users: admin, jellyfin

2. Group: debian-transmission, Users: sonarr,radarr,admin,jellyfin

3. Group: radarr, Users: debian-transmission,sonarr,admin,jellyfin

4. Group: sonarr, Users: debian-transmission,radarr,admin,jellyfin

5. Group: jackett, Users: admin

6. Group: jellyfin, Users: admin,debian-transmission,radarr,sonarr,jackett


## Software Installed with heavy manual config:
1.  Jellyfin media server : https://jellyfin.org

2.  Radarr : https://radarr.video

3.  Sonarr : https://sonarr.tv

4.  Jackett : https://github.com/Jackett/Jackett

5.  Transmission-daemon : https://transmissionbt.com/

6.  Lighttpd + php (basic setup)

7.  Organizr : https://organizr.app/

8.  automount-usb : https://github.com/raamsri/automount-usb

9.  eZServerMonitor : https://www.ezservermonitor.com/ (embedded as an iframe in organizr)

10. automatic-ripping-machine : https://github.com/automatic-ripping-machine/automatic-ripping-machine  (Untested, user switched from arm to admin)

11. MondoRescue : http://www.mondorescue.org

## Extras
As it turns out, [TurnKey Linux](https://www.turnkeylinux.org/) has a canned media server installation CD that does a lot of what I've described above and more! Might want to check that out:

  [Turnkey Linux MediaServer: Simple Network Attached Media Storage](https://www.turnkeylinux.org/mediaserver)

## TODO:
1. Look into usenet downloading.
2. Look into WAN access via openvpn. Don't forward any ports from WAN to LAN (other than bittorrent) - UPDATE: Not connecting as of 20200728. Try after some time...
3. Integrate Radarr and Sonarr with trakt.tv (Google for this).
4. Config mondorescue to backup to iso (http://www.mondorescue.org/docs.shtml)
