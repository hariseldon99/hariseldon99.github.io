# MediaServer Notes
# Table of contents

- [Introduction](#introduction)
- [Summary of required software](#summary-of-required-software)
- [Step 1: Make Ubuntu headless](#step-1-make-ubuntu-headless)
- [Step 2: Install a Media Streaming System:](#step-2-install-a-media-streaming-system)
- [Step 3: Install bittorrent client and indexers:](#step-3-install-bittorrent-client-and-indexers)
- [Step 4: Automounting USB](#step-4-automounting-usb)
- [Step 5: Setup unified interface using Organizr and EasyServerMonitor:](#step-5-setup-unified-interface-using-organizr-and-easyservermonitor)
- [Step 6: Users, Groups and Permissions](#step-6-users-groups-and-permissions)
- [Final Step: Client software](#final-step-client-software)
- [Miscellaneous](#miscellaneous)
- [Extras](#extras)
- [Further Reading](#further-reading)
- [TODO:](#todo)
  
## Introduction
In July, 2020, I setup an old laptop with a busted screen as a Linux media server to download and stream movies and TV episodes over my LAN to various wifi devices (laptops, tablets and smart TVs). Below are the notes of the various steps taken and software installed in order to achieve this.

The details of my old laptop and default setup are given below:

1. Laptop Model: [SAMSUNG model: NP300E5X-U01IN](https://www.samsung.com/in/support/model/NP300E5X-U01IN/)
  
2. Output if [inxi -F](https://smxi.org/docs/inxi.htm):
    
<details>

<summary> CLICK HERE </summary>  

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

</details>
 
3. Detailed hardware specs of this old laptop are hard to find. A detailed datasheet has been obtained from [icecat](https://icecat.lu/). It is referred below:
 
      [icecat: Datasheet for Samsung NP300E5X Notebook](https://icecat.lu/amp/p/vendorName/mpn/desc-19418433.html). 
    
    In case the [link rots](https://www.nngroup.com/articles/fighting-linkrot/), parts of the datasheet table (as of Aug 4, 2020), is reproduced below:

<details><summary>CLICK HERE</summary> <p>

  <table>
    <tr>
        <td>
                                                Processor                                            </td>
    </tr>
    <tr>
        <td>
                                                    Processor manufacturer                                                </td>
        <td>
                                                    Intel                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor model                                                </td>
        <td>
                                                    i3-2310M                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor frequency                                                </td>
        <td>
                                                    2.1 GHz                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor family                                                </td>
        <td>
                                                    2nd gen Intel® Core™ i3                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor cores                                                </td>
        <td>
                                                    2                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor threads                                                </td>
        <td>
                                                    4                                                </td>
    </tr>
    <tr>
        <td>
                                                    System bus rate                                                </td>
        <td>
                                                    5 GT/s                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor cache                                                </td>
        <td>
                                                    3 MB                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor cache type                                                </td>
        <td>
                                                    Smart Cache                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor socket                                                </td>
        <td>
                                                    BGA 1023                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor lithography                                                </td>
        <td>
                                                    32 nm                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor operating modes                                                </td>
        <td>
                                                    64-bit                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor series                                                </td>
        <td>
                                                    Intel Core i3-2300 Mobile series                                                </td>
    </tr>
    <tr>
        <td>
                                                    Processor codename                                                </td>
        <td>
                                                    Sandy Bridge                                                </td>
    </tr>
    <tr>
        <td>
                                                    Bus type                                                </td>
        <td>
                                                    DMI                                                </td>
    </tr>
    <tr>
        <td>
                                                    FSB Parity                                                </td>
        <td>                                        NO
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    Stepping                                                </td>
        <td>
                                                    J1                                                </td>
    </tr>
    <tr>
        <td>
                                                    Motherboard chipset                                                </td>
        <td>
                                                    Intel® HM75 Express                                                </td>
    </tr>
    <tr>
        <td>
                                                    Thermal Design Power (TDP)                                                </td>
        <td>
                                                    35 W                                                </td>
    </tr>
    <tr>
        <td>
                                                    Tjunction                                                </td>
        <td>
                                                    100 °C                                                </td>
    </tr>
    <tr>
        <td>
                                                    Maximum number of PCI Express lanes                                                </td>
        <td>
                                                    1                                                </td>
    </tr>
    <tr>
        <td>
                                                    PCI Express slots version                                                </td>
        <td>
                                                    2.0                                                </td>
    </tr>
    <tr>
        <td>
                                                    PCI Express configurations                                                </td>
        <td>
                                                    1x16,2x8,1x8+2x4                                                </td>
    </tr>
    <tr>
        <td>
                                                    CPU multiplier (bus/core ratio)                                                </td>
        <td>
                                                    21                                                </td>
    </tr>
    <tr>
        <td>
                                                    ECC supported by processor                                                </td>
        <td>                                        No
                                                                                                    </td>
    </tr>
</table>

<table>
    <tr>
        <td>
                                                Memory                                            </td>
    </tr>
    <tr>
        <td>
                                                    Internal memory                                                </td>
        <td>
                                                    4 GB                                                </td>
    </tr>
    <tr>
        <td>
                                                    Internal memory type                                                </td>
        <td>
                                                    DDR3-SDRAM                                                </td>
    </tr>
    <tr>
        <td>
                                                    Memory clock speed                                                </td>
        <td>
                                                    1333 MHz                                                </td>
    </tr>
    <tr>
        <td>
                                                    Memory form factor                                                </td>
        <td>
                                                    SO-DIMM                                                </td>
    </tr>
    <tr>
        <td>
                                                    Memory layout (slots x size)                                                </td>
        <td>
                                                    1 x 4 GB                                                </td>
    </tr>
    <tr>
        <td>
                                                    Memory slots                                                </td>
        <td>
                                                    2x SO-DIMM                                                </td>
    </tr>
</table>

<table>
    <tr>
        <td>
                                                Storage                                            </td>
    </tr>
    <tr>
        <td>
                                                    Total storage capacity                                                </td>
        <td>
                                                    500 GB                                                </td>
    </tr>
    <tr>
        <td>
                                                    Storage media                                                </td>
        <td>
                                                    HDD                                                </td>
    </tr>
    <tr>
        <td>
                                                    Number of HDDs installed                                                </td>
        <td>
                                                    1                                                </td>
    </tr>
    <tr>
        <td>
                                                    HDD capacity                                                </td>
        <td>
                                                    500 GB                                                </td>
    </tr>
    <tr>
        <td>
                                                    HDD interface                                                </td>
        <td>
                                                    SATA II                                                </td>
    </tr>
    <tr>
        <td>
                                                    HDD speed                                                </td>
        <td>
                                                    5400 RPM                                                </td>
    </tr>
    <tr>
        <td>
                                                    Optical drive type                                                </td>
        <td>
                                                    DVD Super Multi DL                                                </td>
    </tr>
    <tr>
        <td>
                                                    Card reader integrated                                                </td>
        <td>
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    Compatible memory cards                                                </td>
        <td>
                                                    SD,SDHC,SDXC                                                </td>
    </tr>
</table>
<table>
    <tr>
        <td>
                                                Graphics                                            </td>
    </tr>
    <tr>
        <td>
                                                    Discrete graphics adapter model                                                </td>
        <td>
                                                    NVIDIA® GeForce® GT 620M                                                </td>
    </tr>
    <tr>
        <td>
                                                    On-board graphics adapter                                                </td>
        <td>
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    Discrete graphics adapter                                                </td>
        <td>
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    On-board graphics adapter family                                                </td>
        <td>
                                                    Intel® HD Graphics                                                </td>
    </tr>
    <tr>
        <td>
                                                    On-board graphics adapter model                                                </td>
        <td>
                                                    Intel® HD Graphics 3000                                                </td>
    </tr>
    <tr>
        <td>
                                                    On-board graphics adapter base frequency                                                </td>
        <td>
                                                    650 MHz                                                </td>
    </tr>
    <tr>
        <td>
                                                    On-board graphics adapter dynamic frequency (max)                                                </td>
        <td>
                                                    1100 MHz                                                </td>
    </tr>
    <tr>
        <td>
                                                    On-board graphics adapter ID                                                </td>
        <td>
                                                    0x116                                                </td>
    </tr>
    <tr>
        <td>
                                                    Discrete graphics memory type                                                </td>
        <td>
                                                    GDDR3                                                </td>
    </tr>
</table>

<table>
    <tr>
        <td>
                                                Network                                            </td>
    </tr>
    <tr>
        <td>
                                                    Wi-Fi                                                </td>
        <td>
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    Bluetooth                                                </td>
        <td>
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    Wi-Fi standards                                                </td>
        <td>
                                                    802.11b,802.11g,Wi-Fi 4 (802.11n)                                                </td>
    </tr>
    <tr>
        <td>
                                                    Ethernet LAN                                                </td>
        <td>
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    Ethernet LAN data rates                                                </td>
        <td>
                                                    10,100,1000 Mbit/s                                                </td>
    </tr>
    <tr>
        <td>
                                                    Bluetooth version                                                </td>
        <td>
                                                    4.0                                                </td>
    </tr>
    <tr>
        <td>
                                                    Data network                                                </td>
        <td>
                                                    Not supported                                                </td>
    </tr>
    <tr>
        <td>
                                                    Cabling technology                                                </td>
        <td>
                                                    10/100/1000Base-T(X)                                                </td>
    </tr>
    <tr>
        <td>
                                                    4G WiMAX                                                </td>
        <td>
                                                                                                    </td>
    </tr>
    <tr>
        <td>
                                                    Networking standards                                                </td>
        <td>
                                                    IEEE 802.11b,IEEE 802.11g,IEEE 802.11n                                                </td>
    </tr>
</table>
</p> </details>

The key requirements of my home media server are as follows:

  1. That it have a [DLNA](https://windowsreport.com/dlna-servers/) and web-based streaming service for hosting downloaded content on the LAN
  
  2. That it have web based interface to indexer software that searches bittorrent indexes online for content, then download it automatically,
  
  3. That it have a bittorrent client running that has a web based frontend for the benefit of the indexers,
  
  4. That it have a web-based tool to configure and monitor all of the above, 
  
  5. That it have a basic SSH setup, 
  
  6. That it use [hardware transcoding](https://www.streamingmedia.com/Articles/Editorial/Featured-Articles/Hardware-Based-Transcoding-Solutions-Roundup-Testing-Performance-134039.aspx) of audio and video using the onboard NVIDIA graphics card,
  
  7. That it automatically mounts any USB storage devices attached to it (for manually copying content), and
  
  8. ~~That it [automatically rip any DVD](https://www.toptenreviews.com/what-is-the-difference-between-dvd-ripping-and-copying) placed in the DVD drive and allow the content to be streamed.~~ (This is now moot, as I swapped out the dvd drive for an extra HDD using a [laptop hard drive caddy](https://youtu.be/H09SEyoE8yY).


To these ends, I stripped down my Ubuntu installation from standard to barebones, so that it can run headless without starting X. Then reinstall the nvidia graphics drivers with X so that they're running at least, then setup ssh and remote-login, then setup all the abovementioned software. Note that the servers are not natted to WAN for security reasons.

## Summary of required software

This is the order in which the tasks should be done.

1.  Headless Ubuntu: https://help.ubuntu.com/community/Installation/MinimalCD

2.  Transmission-daemon : https://transmissionbt.com/

3.  Jellyfin media server : https://jellyfin.org

4.  Jackett : https://github.com/Jackett/Jackett

5.  Radarr : https://radarr.video

6.  Sonarr : https://sonarr.tv

7.  Organizr : https://organizr.app/

8.  eZServerMonitor : https://www.ezservermonitor.com/ (embedded as an iframe in organizr)

9.  automount-usb : https://github.com/raamsri/automount-usb

## Step 1: Make Ubuntu headless


First, I made my existing ubuntu install [headless](https://smallbusiness.chron.com/headless-linux-33715.html) so that it runs in console mode without graphics. Strictly speaking, this is not necessary, but I believe that not running unnecessary graphics will free up some cpu and RAM for streaming, and have extra HDD space for media.

To make an existing ubuntu headless, follow the instructions in the link below:

[Turn Ubuntu desktop into an headless server](https://ubuntuusertips.wordpress.com/2014/02/19/turn-ubuntu-desktop-into-an-headless-server/)

For a fresh install, I suspect that the [ubuntu MinimalCD](https://help.ubuntu.com/community/Installation/MinimalCD) is the best option. Simply boot off it and install only basic packages and internet-wifi connection stuff, no graphics or X11/wayland needed at this juncture.

Then, maintain the internet connection and auto-install the nVidia graphics drivers from the command line as per instructions given below

[2 Ways to Install nVidia Driver on Ubuntu 18.04 (GUI & Command Line)](https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04)

Note that the kernel headers corresponding to the RUNNING KERNEL must be installed. This can be done with the command

```console
sudo apt install linux-headers-$(uname -a|awk '{print $3}')
```

Install and setup the SSH server, and setup the '/etc/issue' file and ubuntu custom message for logins as per the introduction section:

See this HOWTO:

[How to Enable SSH on Ubuntu 18.04](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/)

## Step 2: Install a Media Streaming System:
There are several media streaming servers for Linux, the most popular ones (as of 2020), being [Plex](https://www.plex.tv/) and [Emby](https://emby.media/). I tried both of them. However, Plex was beset with networking difficulties, and [disallowed hardware transcoding unless you paid for their premium service](https://support.plex.tv/articles/115002178853-using-hardware-accelerated-streaming/). Furthermore, Emby is [crippleware](https://web.archive.org/web/20090111094411/http://home.att.net/~srschmitt/jargonfile/jargon_file-152.html); you have to pay premium for using any client on a smart TV. Thus, I settled for the open source fork of Emby, called [Jellyfin media server](https://jellyfin.org).

### Install Jellyfin
Install Jellyfin as per instructions here:

[Jellyfin Quick Start: Installing on Ubuntu](https://jellyfin.org/docs/general/administration/installing.html#ubuntu)

### Hardware Transcoding with nVidia GPUs

If you have an nVidia graphics card that supports hardware transcoding (research your model, mine does not), then enable hardware transcoding with [nVidia NVENC/NVDEC](https://developer.nvidia.com/nvidia-video-codec-sdk) and the version of FFMPEG bundled with Jellyfin. Instructions are below.

[Jellyfin Quick Start: Hardware Acceleration](https://jellyfin.org/docs/general/administration/hardware-acceleration.html)

### Hardware Transcoding with intel GPUs
Turns out that my M-series nVidia GPU **does not support hardware transcoding**. I learnt this the hard way by trying the config in the previous subsection and failing. To check whether your hardware transcoding is working, check the logs in "/var/log/jellyfin". There are transcode logs named "ffmpeg-transcode-XXXXXX" where "XXXXX" is some sort of hash. Go ahead and grep through them or just open them up in a text editor or whatever. See [this section](https://jellyfin.org/docs/general/administration/hardware-acceleration.html#verifying-transcodes) in the HOWTO cited in the previous subsection of this doc for details.

Nonetheless, hardware transcoding is possible in standard Intel graphics cards using the open source [VAAPI](https://www.freedesktop.org/wiki/Software/vaapi/) libraries. For instructions on how to get Jellyfin to do it, see the HOWTO below:

[Jellyfin Quick Start: Hardware Acceleration using VAAPI](https://jellyfin.org/docs/general/administration/hardware-acceleration.html#configuring-vaapi-acceleration-on-debianubuntu-from-deb-packages)

Usually, once the intel graphics drivers are up and running, Jellyfish can automatically choose the codecs that are supported by the GPU once VAAPI is enabled in the "Transcoding" configuration page (see the subsection below on where to find it). In any case, if you need to know which codecs are supported for your card, then go through the HOWTO cited below:

[archlinux wiki: Hardware Video Acceleration](https://wiki.archlinux.org/index.php/Hardware_video_acceleration#Verifying_VA-API)

### Hardware Transcoding: Multiple GPU systems
If you have multiple graphics cards with one of them being an [nVidia optimus-](https://www.nvidia.com/en-us/geforce/technologies/optimus/)compatible gpu, you may install the nVidia graphics drivers the standard way and use [PRIME profiles](https://wiki.archlinux.org/index.php/PRIME) to switch them around. See the HOWTO in the link below for a simple introduction:

[LinuxBabe: How To Switch Between Intel and Nvidia Graphics Card on Ubuntu](https://www.linuxbabe.com/desktop-linux/switch-intel-nvidia-graphics-card-ubuntu)

### RAM Transcoding

Finally, I opted for RAM transcoding, where transcoded files are written to RAM instead of disk for faster access. For background, checkout the youtube video below (this one is for Plex, but the principle is the same for all streaming servers)

   [![5 Ways to optimize your Plex Media Server](https://img.youtube.com/vi/F_Pc_4SahWg/0.jpg)](https://www.youtube.com/watch?v=F_Pc_4SahWg)
   
 To create a ramdisk and mount it on ubuntu, follow this HOWTO:
 
 [How to Create and Use a Ramdisk on Ubuntu 18.04](https://linuxhint.com/ramdisk_ubuntu_1804/)
 
 I chose to mount it on the path '/var/lib/jellyfin/transcodes', the default location where jellyfin stores transcoded data. If you need to use any other path, then the settings can be obtained by navigating in the Jellyfish Home page as follows: Navigation menu on the left + "Admin : Dashboard --> Playback --> Transcoding (top of the page)"
 
 ![Transcoder Settings](transcoder_settings.png)

  As can be seen in the screenshot above, the transcoder setting can be used to enable VAAPI transcoding as described in the Jellyfin "Quick Start" page (linked above) on Hardware Acceleration.
  
## Step 3: Install bittorrent client and indexers:

1. Bittorrent client: I've chosen [transmission](https://transmissionbt.com/), but there are other clients with remote interfaces (see [Extras](#extras)). Installing transmission without a GUI (headless) and running the web interface can be done as per the instructions below:

    [How to set up transmission-daemon on a Raspberry Pi and control it via web interface](https://linuxconfig.org/how-to-set-up-transmission-daemon-on-a-raspberry-pi-and-control-it-via-web-interface). Note that it doesn't have to be done in a raspberry pi. The instructions will work on any computer running Debian or Ubuntu Linux.

2. Bittorrent indexers: For movies, I chose to install [Radarr](https://radarr.video/) and for TV shows, I chose [Sonarr](https://sonarr.tv/). For details on setting them up. check out their GitHub pages:

    a. Radarr: [GitHub Page](https://github.com/Radarr/Radarr)
  
    b. Sonarr: [GitHub Page](https://github.com/Sonarr/Sonarr)
  
   Note that you will have to setup supported online indexers for bittorrent. There are only a few for Radarr and Sonarr, and they don't always work well. Therefore, I also installed the Jackett proxy server which connects to thousands of online indexers and configured radarr and sonarr to use Jackett instead. For instructions, checkout the [GitHub page for jackett](https://github.com/Jackett/Jackett). Also, see [this section](#bypass-cloudflare-protection) for details on how to use [flaresolverr](https://github.com/FlareSolverr/FlareSolverr) with jackett to bypass bot checks.
 
  For further details, checkout these HOWTOs:
 
   * [How to use Jackett with Sonarr](https://community.seedboxes.cc/articles/how-to-use-jackett-with-sonarr)
  
   * [Sonarr – How to add good Public Indexers](https://tricksty.com/tricks/sonarr-how-to-add-good-public-indexers)
  
   * [Installing Radarr, Sonarr and Deluge on your Unraid Server](https://blog.harveydelaney.com/installing-radarr-sonar-and-deluge-on-your-unraid-setup/)


Indexers enabled in Jackett:

![Indexers Enabled](image.png)


## Step 4: Automounting USB

Here, I wanted to setup the media server in such as way that inserting a USB thumb drive or external hard drive into the machine would automatically mount it without manual intervention. This way, I can remotely log in and just copy the files from the drives to wherever. The simplest way is to use Ubuntu's systemd to launch the automount service at boot, the service being [automount-usb](https://github.com/raamsri/automount-usb). Simply checkout the github repository and follow the instructions therein

  ```console
  $ git checkout https://github.com/raamsri/automount-usb
  $ cd automount-usb
  $ sudo ./CONFIGURE.sh
  ```


## Step 5: Setup unified interface using Organizr and EasyServerMonitor:
Phew! That was a lot of installations and configs! Now, the media server has a lot of web services running in all sorts of ports, with more possibly in the future. How does one keep track of it all? Bookmarks in the browser? UGH! What about checking up on server status? Do we just keep ssh-ing periodically? How crude!

An excellent software for keeping all your media services together for easy viewing and configuration is called ["Organizr"](https://organizr.app/). It sets up a web login using PHP on an standard web server where you can keep all your media service links in one place and see a status dashboard to boot! Head on over to [their documentation](https://docs.organizr.app/) and follow the installation instructions. Alternatively, see the following article (adjust for your operating system)

  [The Ultimate Organizr V2 Setup Guide for Windows](https://smarthomepursuits.com/install-organizr-v2-windows/)

The above-mentioned instructions can be readily adapted to Ubuntu. I would recommend installing the latest development version, as it has more features than the stable version. 

Finally, an interesting trick can be to run a simple PHP-web based system monitor and enbed the output on your organizr home page. I chose [eZServerMonitor](https://www.ezservermonitor.com/) due to its simplicity and low footprint. Install it in a subdirectory of your organizr install, then open Organizr page in your browser, go to 'settings -> Tab Editor -> Homepage Items -> CUSTOMHTML-1' and input the following html markup tag 
  
     ```html
        <iframe src="http://192.168.1.2/apps/ezservermonitor/index.php" name="System Monitor" height="1400px" width="100%" title="System Monitor"></iframe>
     ```
  Once this is saved and enabled, the Organizr homepage should show a nice big embedded frame with all your machine status information in it.
     
  This is what my Organizr Homepage looks like   
  ![Organizr Homepage](Screenshot%20from%202020-08-28%2019-04-00.png)
     
## Step 6: Users, Groups and Permissions

Finally, since all the different softwares installed above often want to communicate content data to each other in disk, I thought it best to let them. To that end, each software creates a user and group with the same name as the software (this is done automatically). Set the working directories of each of the following software to permissions where the user and group gets to read, write and execute, and assign  the groups to each other. Consult standard linux documentation on how to do this. The following users/groups are important in this regard:

1. Group: admin, Users: admin, jellyfin

2. Group: debian-transmission, Users: sonarr,radarr,admin,jellyfin

3. Group: radarr, Users: debian-transmission,sonarr,admin,jellyfin

4. Group: sonarr, Users: debian-transmission,radarr,admin,jellyfin

5. Group: jackett, Users: admin

6. Group: jellyfin, Users: admin,debian-transmission,radarr,sonarr,jackett

## Final Step: Client software
Finally, of course, we'll need clients to connect and stream from the Jellyfin server. The clients page of the Jellyfin website has a lot of information on this:

[Jellyfin Clients](https://jellyfin.org/clients/)

You can also use any web browser and connect via organizr. In any case, clients exist for several operating systems and smart media devices ranging from Android TVs to Amazon Fire-TV. If none of them work, then enable the [DLNA server in Jellyfish](https://jellyfin.org/docs/general/networking/dlna.html) in the Media Server and use any DLNA-compatible video player in your device to detect and connect to it. Many such players exist for all sorts of operating systems. A good Open Source one is [VLC](https://www.videolan.org/), also supported on [Android and Amazon Fire TV](https://www.videolan.org/vlc/download-android.html).


## Miscellaneous

### Content of /etc/issue:
  
<details>
  
  <summary> CLICK HERE</summary> 
  
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
  * USB Drives :    USB drives are automatically detected and mounted
 ```
</details>
 
### Content of custom message during remote login
 
 <details>
  
  <summary> CLICK HERE </summary>
  
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
    printf " * USB Drives :    USB drives are automatically detected and mounted\n"
```
</details>

### Maintenance

It goes without saying that this machine is running 24/7. Laptops are generally not designed for continuous running and the cpu can run fairly hot. It is important to manage this as well as possible. The best way is to install fan control software that adjusts the speed of the cpu fan to maximize cooling. There are numerous software for this on linux (google for them). The standard [lm-sensors](https://github.com/lm-sensors/lm-sensors) tool does not detect my cpu fan no matter what. Thus, I have chosen to try "[samsung-tools](https://loms.voria.org/viewtopic.php?p=5798#p5798)", a general toolkit designed for samsung laptops using the .

Samsung-tools for linux can set the fan speed to 'overclock' mode, where the fan presumably cools more aggressively. However, the setting seems to be non-persistent, meaning it disappears after a reboot. Therefore, I've setup a [user-level cron job](https://help.ubuntu.com/community/CronHowto) to set it to overclock mode at bootup. This should, in principle, maximize cooling. The software can be installed on ubuntu from the PPA given below:

[Linux On My Samsung](https://launchpad.net/~voria/+archive/ubuntu/ppa)

Simply run
  ```console
  $ sudo add-apt-repository ppa:voria/ppa && apt install samsung-tools
  ```
Note that samsung-tools needs [D-Bus](https://dbus.freedesktop.org/doc/dbus-tutorial.html) to work, so cron can't directly run it unless it has logged in as a user. An ugly hack for this is a  cron job like

```console
@reboot sleep 20 && ssh localhost samsung-tools -c overclock 
```

where ssh has been setup for login by key pairs locally. [See this howto](https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/) for that.

Also, I thought it a good idea to downclock the CPU in order to minimize overheating. Doesn't seem to effect transcoding or streaming. Do this with [cpufrequtils](http://www.thinkwiki.org/wiki/How_to_use_cpufrequtils) as follows

  ```console
  $ sudo apt-get install cpufrequtils
  $ echo 'GOVERNOR="powersave"' | sudo tee /etc/default/cpufrequtils
  $ sudo systemctl disable ondemand
  ```

## Extras

### Bypass Cloudflare protection

As of June 2020, a lot of torrent indexer websites are protected by services like [cloudfare](https://www.cloudflare.com) and others. These online services prevent bots (like [Jackett](https://github.com/Jackett/Jackett), which I had recommended for automatically searching for torrents while [installing indexers](#step-3:-Install-bittorrent-client-and-indexers:)) from accessing these sites by putting in automatic Turing tests and/or [CAPTCHAS](https://www.pandasecurity.com/en/mediacenter/panda-security/what-is-captcha/) designed for manual intervention. As it happens, the fella developing Jackett has created a workaround called [flaresolverr](https://github.com/FlareSolverr/FlareSolverr). This is a software that runs as a service, and Jackett can connect to it, have it launch a [headless chromium browser session](https://chromium.googlesource.com/chromium/src/+/lkgr/headless/README.md) and try to fool the bot blockers into thinking that it is a human. It's not follproof, but increasingly necessary as many torrent sites are getting bot blockers to prevent malicious hackers from crashing their sites. The github page of flaresolverr instructs how to set it up, but does not have a way to startup on boot. On Ubuntu, the following systemd script should do it. Assuming that flaresolverr has been unpacked to "/usr/local/flaresolverr", simply create the file "/etc/systemd/system/flaresolverr.service" and add:

```console
 [Unit]
Description=Systemd service script for flaresolverr

Wants=network.target
After=syslog.target network-online.target

[Service]
Type=simple
ExecStart=/usr/local/flaresolverr/flaresolverr
Restart=on-failure
RestartSec=10
KillMode=process

[Install]
WantedBy=multi-user.target

 
 ```

Then, run the following:

```console
  $ sudo chmod 640 /etc/systemd/system/flaresolverr.service
  $ sudo systemctl daemon-reload
  $ sudo systemctl enable flaresolverr
  $ sudo systemctl start flaresolverr
  ```
 That's it. In case any other configuration is required, then the systemd script can be modified accordingly.

### Automatic DVD ripping:

If you have a DVD drive in your system, you can setup the system to automatically mount and rip any inserted DVD discs and copy the content files over to a separate folder in the Jellyfin media user space. To do that, I setup [Automatic Ripping Machine (ARM)](https://b3n.org/automatic-ripping-machine/). Just check out the [relevant GitHub page](https://github.com/automatic-ripping-machine/automatic-ripping-machine) and follow the instructions therein.

### Integration with Trakt

Trakt is an online platform that primarily keeps track of TV shows and movies you watch. It integrates with your media center or home theater PC to enable scrobbling, so everything is automatic. You can create a trakt account at (https://trakt.tv/), create empty lists of movies and have radarr and sonarr automatically download items from them once they get populated. 

 * While trakt lists can be added directly to radarr from the "List" option in radarr's settings, this cannot (as of August 10, 2020) be done with Sonarr. Until that happens, probably best to install and run [traktarr](https://github.com/l3uddz/traktarr) as a service that periodically scans yout trakt lists for content to add to radarr and sonarr. Check out the GitHub page linked above for setup instructions. Note that the configuration file is a [json file](https://www.json.org/), and needs extensive manual editing. For some background on the structure of json files (they're similar to python dictionaries), [see this introduction](https://www.digitalocean.com/community/tutorials/an-introduction-to-json)

 * You can also [scrobble](https://www.wired.com/2012/11/richard-jones-scrobbling/) your movies and shows from Jellyfin to trakt with the [Trakt plugin for Jellyfin](https://github.com/jellyfin/jellyfin-plugin-trakt).

### Bittorrent thin clients
The web interface for the [transmission bittorrent client](https://transmissionbt.com/) is a bit basic. You can enhance it with a better web interface, or use a client from another machine to connect to it. Details are available in the [web site of transmission itself](https://transmissionbt.com/resources/). I've tried [transmission web control](https://github.com/ronggang/transmission-web-control/wiki). 

Alternatively, you can try more sophisticated bittorrent clients with more detailed web interfaces. Examples are [deluge](https://deluge-torrent.org/) and [qbittorrent](https://www.qbittorrent.org/). However, transmission, coded mainly in C/C++, [has the lowest resource usage of all bittorrent clients](https://transmissionbt.com/about/). Deluge, coded in python, consumes much more memory. Qbittorrent is written in C++, and is, by accounts, pretty lean, although I have not tried it. [See this link](https://www.linuxbabe.com/ubuntu/install-qbittorrent-ubuntu-18-04-desktop-server) for headless config for qbittorrent.

### Additional downloaders
In addition to bittorrent, I'm experimenting with other downloaders [p2p](https://techterms.com/definition/p2p) networks. The Radarr and Sonarr PVR applications only support bittorrent and usenet, as far as I know. In addition, I have tried the following independently

 * [Amule](https://www.amule.org/): A p2p application mainly accessing the [EDonkey and Kad networks](https://www.freezenet.ca/guides/filesharing-and-distribution/how-to-connect-to-the-ed2k-and-kad-networks-emule/): 
 
      * Set it up as a daemon and run it as user "amule" with home directory at "/var/lib/amuled". See this [howto](https://linuxconfig.org/how-to-setup-amule-and-control-it-via-web-interface-on-a-raspberry-pi) for details. Again, it's not exclusively meant for a Raspberry Pi. [See this wiki](https://wiki.amule.org/wiki/Getting_Started) for getting started with amule. 
      
      * You may also need the [non-web remote gui](http://wiki.amule.org/wiki/FAQ_amulegui) for initial access and config. 
      
      * Note that radarr, sonarr, lidarr etc do not integrate with edonkey or any other p2p network besides usenet and bittorrent. As a workaround, set the [incoming folder of amule downloads](https://wiki.amule.org/wiki/AMule_files#Directories) to wherever (I have it set to /var/lib/amuled/.aMule/Incoming), then install the ["Auto Organnize Plugin"](https://jellyfin.org/docs/general/server/plugins/index.html#auto-organize) to Jellyfin and have it monitor the amule download folder for content, which it then integrates into Jellyfin's Libraries. This way, I can manually set downloads and they, at least, get integrated into Jellyfin properly.
  
  * [Youtube Downloader](https://ytdl-org.github.io/youtube-dl/) with a nice [php-web interface](https://github.com/outkastm/Youtube-dl-WebUI). If you've got nginx setup already then simply clone the repository into your website.
  
### Reverse Proxy
The configurations above basically install a bunch of servers that have to be accessed directly using the url and port numbers. This can be a problem since firewalls will have to allow traffic into those ports, and WAN access is unsafe without encrryption. If you want WAN access to your server, then it is better to set up all services via [reverse proxies](https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy/) in [nginx](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/). See this document for a decent guide on reverse proxying all these services.

 * [How to Setup a Reverse Proxy in OMV with Let’s Encrypt SSL for Sabnzbd, Radarr, Sonarr and Transmission](https://daan.dev/how-to/reverse-proxy-omv-letsencrypt-sabnzbd-radarr-sonarr-transmission/3/)

### TurnKey Linux MediaServer
As it turns out, [TurnKey Linux](https://www.turnkeylinux.org/) has a canned media server installation CD that does a lot of what I've described above and more! Might want to check that out:

  [Turnkey Linux MediaServer: Simple Network Attached Media Storage](https://www.turnkeylinux.org/mediaserver)
 It just means that it can't verify the SSl certificate you generated before. It'll still work. Just proceed to the server even if it is labelled unsafe.
 
## Further Reading:

* [HTPC Download Box](https://github.com/sebgl/htpc-download-box) - Same basic setup as this one, but with dockers

* [Smart Home Beginner](https://www.smarthomebeginner.com/)

## TODO:

1. Look into WAN access via reverse proxy.

   * Have not configged SSL yet. WAN forwarding is currently still disabled.
   * Problem is authentication. Radarr, Sonarr, Lidarr, jackett and Transmission all have independent authentication (all are presently disabled, so exposing them to internet is risky) and needs to be maintained separately. Only Jellyfin and Organizr can have synchronized authentication.
   * All Authentication can be done via LDAP + nginx reverse proxy. Organizr and jellyfin can use LDAP directly, all else can use secure LDAP via nginx. Can also add shellinabox.
      * https://riegers.in/nextcloud-using-a-reverse-proxy/
      * https://icicimov.github.io/blog/web%20server/Nginx-LDAP-module/
      * https://ubuntu.com/server/docs/service-ldap

2. Organizr acts like ddos when nginx is configged with fail2ban with ddos protection. Ip gets banned unless whitelisted.
