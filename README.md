# Nixos Journey

## Background Info

I have been using Linux for about 2 years now: 1 year on EndeavourOS (using XFCE) and 1 year on Arch Linux (the first half year I used i3 and the second half year I used Hyprland). For others reading, this is a warning that I might skip over some things but just let me know if you want more info on something (create an issue?) and I'll update this journal/guide. Hopefully I'll keep adding to this and will make this clearer and more robust.

In addition, I have used NixOS once before during the school year, but only for around a week, so I never was able to properly use it. I'm going to document my journey using NixOS here since the documentation isn't the best and it's kinda confusing watching videos that don't really build off each other. The reason why it's hard to follow videos that don't build off each other is that they often use different things and are set up differently, such as some use home manager or flakes, others don't.

Also, I want to look back over what I've done on my system in case I have no idea what I previously did; it'll help me understand my previous saves. This is public so hopefully it'll help someone as confused as I am.

### Note

I am dual booting NixOS with Windows on two SSD's and am using a data partition so both operating systems can access some of the same files. 

How I'm setting my laptop up: (I don't think it matters which SSD Windows and NixOS are on)

256 GB SSD:
* Windows

512 GB SSD:
* NixOS
* data partition

Also, I'm using a Thinkpad E14 Gen 4 which I have wiped multiple times to use Windows and NixOS (it's a long story) so I'm treating my laptop as if I'm installing on a new system with no data (so make sure to back up your data).

## Where to Start

tbh I forgot what I was gonna put here so I'll hopefully remember what to put here later

anyways, this can prob act as a table of contents

## Installing Windows

(When I say Linux, it means any Linux OS, including NixOS)

Since Windows can only be installed on an entire SSD, not on a drive partition, Windows should be installed first.

(it might not matter if it's on its own SSD such as with my case but it's better to be on the safe side and install Windows before Linux)
(if Windows and Linux are to be installed on the same SSD, Windows must be installed first)

Anyways, if you don't already have Windows installed, on another Windows device, install the [Windows 11 ISO](https://www.microsoft.com/en-us/software-download/windows11) or the [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10ISO). While that's downloading, download [Rufus](https://rufus.ie/en/). Once everything is finished downloading, use Rufus to flash the Windows ISO to the flash drive.

On the device you wanna download Windows and NixOS to, use the installer from the flash drive to install Windows how you want to.

## Installing NixOS

If you skipped to here, you can use [Rufus](https://rufus.ie/en/) to flash an ISO to a flash drive on Windows.

To [download NixOS](https://nixos.org/download/), go to the 'NixOS : the Linux distribution' section and install one of the ISO images that fit your system. I'm using the 'GNOME, 64-bit Intel/AMD' installer, but the Plasma Desktop and minimal ISO image installers should work fine.

Use Rufus to flash the ISO onto the flash drive and then boot into it. I'm using the GNOME installer so I'll go through that.

### Parting the Disk
