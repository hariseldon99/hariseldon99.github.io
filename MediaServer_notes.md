# MediaServer Notes

## Stuff Installed with heavy manual config:
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

## Special system users/groups. All listed users belong to all listed groups and homedirs are writable to all

1. sshd:x:123:65534::/run/sshd:/usr/sbin/nologin
2. admin:x:1002:1002:ADMINISTRATOR,,,:/home/admin:/bin/bash
3. debian-transmission:x:121:125::/var/lib/transmission-daemon:/usr/sbin/nologin
4. radarr:x:998:998::/var/lib/radarr:/usr/sbin/nologin
5. sonarr:x:111:1003::/var/lib/sonarr:/usr/sbin/nologin
6. jackett:x:997:997::/var/lib/jackett:/usr/sbin/nologin
7. jellyfin:x:122:128:Jellyfin default user,,,:/var/lib/jellyfin:/bin/false

## HOWTOS:
1.  https://tricksty.com/tricks/sonarr-how-to-add-good-public-indexers
2.  https://www.loggly.com/ultimate-guide/linux-logging-with-systemd/
3.  https://www.golinuxcloud.com/systemd-journald-how-logging-works-rhel-7/
4.  https://websiteforstudents.com/setup-lighttpd-web-server-with-php-supports-on-ubuntu-servers/
5.  https://community.wd.com/t/guide-auto-removal-of-downloads-from-transmission-2-82/93156
6.  https://smarthomepursuits.com/install-organizr-v2-windows/
7.  https://linuxhint.com/ramdisk_ubuntu_1804/ (for RAM transcoding)
8.  https://jellyfin.org/docs/general/administration/hardware-acceleration.html

## TODO:
1. Look into usenet downloading.
2. Look into WAN access via openvpn. Don't forward any ports from WAN to LAN (other than bittorrent) - UPDATE: Not connecting as of 20200728. Try after some time...
3. Integrate Radarr and Sonarr with trakt.tv (Google for this).
4. Config mondorescue to backup to iso (http://www.mondorescue.org/docs.shtml)

## Notes:
