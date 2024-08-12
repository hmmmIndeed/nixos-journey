# Nixos Journey

## Background Info

I have been using Linux for about 2 years now: 1 year on EndeavourOS (using XFCE) and 1 year on Arch Linux (the first half year I used i3 and the second half year I used Hyprland). For others reading, this is a warning that I might skip over some things but just let me know if you want more info on something (create an issue?) and I'll update this journal/guide. Hopefully I'll keep adding to this and will make this clearer and more robust (correct me if something is wrong though). Also, I am purposely adding redundancy if it helps make something clearer.

In addition, I have used NixOS once before during the school year, but only for around a week, so I never was able to properly use it. I'm going to document my journey using NixOS here since the documentation isn't the best and it's kinda confusing watching videos that don't really build off each other. The reason why it's hard to follow videos that don't build off each other is that they often use different things and are set up differently, such as some use home manager or flakes, others don't. Keep in mind that since there are so many ways to set up NixOS that mine is only one way and it may not be the best way.

Also, I want to look back over what I've done on my system in case I have no idea what I previously did; it'll help me understand my previous saves. This is public so hopefully it'll help someone as confused as I am.

### Note

I am dual booting NixOS with Windows on two SSD's and am using a data partition so both operating systems can access some of the same files (which are the files in the partition).

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

### Welcome, Location, and Keyboard

Just choose your language, location, and keyboard. Usually whatever the default is will be correct but change it if needed.

### Users

Add your name, username, user password, and admin (root) password. Here's a good explaination on [name vs username](https://askubuntu.com/a/399556) in case you're confused.

### Desktop

I will be using Hyprland so I will choose the 'No desktop' option; you choose whatever you want. 

### Unfree Software

I recommend you check the 'Allow unfree software' checkbox in the 'Unfree Software' section.

### Partitions

If you're using multiple SSD's, make sure you're using the correct SSD. If the SSD is blank and/or new, create a new parition table and format it as GPT.

To install NixOS, you need at least two partitions: the boot partition and the one with NixOS (the / parition). A swap partition and a data partition aren't required for NixOS but will be nice if you wanna use them.

Required Partitions:
* Boot Partition: Generally, a boot partition can be under 500 MB but mine is 1 GB just in case. It should also be FAT32 and have a mount point of /boot. Also, flag it as boot.
* Root Partition: This partition should be how ever much space you want for NixOS which is usually the rest of the storage on the SSD. It should be ext4 and have a mount point of /.

Optional Partitions:
* Swap Partition: It can be used for virtual memory ([when the hard drive is used for memory](https://wiki.archlinux.org/title/swap)) and/or hibernation ([saves machine state to the swap partition and powers the machine off](https://wiki.archlinux.org/title/Power_management/Suspend_and_hibernate)). I used [this](https://askubuntu.com/a/49138) to decide how much storage my swap parition should take. I have 16 GB of RAM and want to use hibernation (which btw only really useful for laptop since it saves power in contrast to sleep) so my swap partition is 24 GB. Also, flag it as swap.
* Data Partition: I'm using this to store data that both NixOS and Windows can access. It must be NTFS so windows can access it (it'll be under the D: parition instead of the usual C: partition). I just used the rest of my SSD for this partition so leave it as unformatted when installing NixOS. **Don't create this partition when installing NixOS!!! You must do it later!!!**

![image](https://github.com/hmmmIndeed/nixos-journey/assets/73439762/91c0191b-0d4a-4406-aad3-f0f642e88389)

The partitions in that order are: boot, swap, root, and data

### Summary, Install, and Finish

Make sure everything is correct and press the 'Install' button. It'll take a bit to install NixOS but once it finishes you're ready to go!

If you want a data partition, open GParted, switch to the correct SSD if it's not already on it, and choose the unformatted space. Make it NTFS and then format it.

## Setting Up NixOS

To start off, I used quite a few resources for this part so I'm just going to link them here:

[Nixos and Hyprland - Best Match Ever](https://www.youtube.com/watch?v=61wGzIv12Ds) by Vimjoyer


The NixOS configuration files that come with the system are located in ```/etc/nixos``` and the two default files are ```configuration.nix``` and ```hardware-configuration.nix```. ```hardware-configuration.nix``` should be left alone so all the configuration will happen in ```configuration.nix``` and other files you'll make.

I would also recommend connecting to the Internet with ```nmtui```.

Use these commands to access ```configuration.nix``` (I like cd'ing into the directory first)

    cd /etc/nixos
    sudoedit configuration.nix

If you plan on using Hyprland, add these lines to your ```configuration.nix```:

This enables Hyprland

    programs.hyprland.enable = true;

which is the same thing as

    programs.hyprland = {
      enable = true;
    };

but with different syntax.

For example, ```i.am.not.john = true;``` is the same as

    i.am.not = {
      john = true;
    }

and

    i.am = {
      not.john = true;
    }

and

    i.am = {
      not = {
        john = true;
      }
    }

You get the idea. Anyways, once that Hyprland stuff is added, save the file and rebuild and switch to that new version with

    sudo nixos-rebuild switch

### Flakes

The purpose of flakes is it's what allows your system to be truely reproduceable. To enable it, add this line into ```configuration.nix```:

    nix.settings.experimental-features = [ "nix-command" "flakes" ];

I like putting it under the area where the hostname is defined but it shouldn't matter where it is.

Next, save the file and run

    sudo nixos-rebuild switch

Now that flakes are enabled, run this to create a simple example flake in your directory. This can be used as a template to create your first flake.

    sudo nix flake init

Now let's change it to the code below, replaceing <hostname> with the hostname of your system (if you're not sure, just run ```hostname``` in the terminal)

    {
      description = "A very basic flake";
    
      inputs = {
        nixpkgs.url = "github:nixos/nixpkgs?ref=nixos-unstable";
      };
  
      outputs = { self, nixpkgs, ... }:
        let
          lib = nixpkgs.lib;
        in {
        nixosConfigurations = {
          <hostname> = lib.nixosSystem {
            system = "x86_64-linux";
	        modules = [./configuration.nix];
          };
        };
      };
    }

I'll break the nix code down for you.

### HomeManager

Here's a good vid: https://www.youtube.com/watch?v=IiyBeR-Guqw

It does have an error in it, with the errored line in flake.nix commented out

    {
      description = "A very basic flake";
    
      inputs = {
    #    nixpkgs.url = "github:nixpkgs/nixos-unstable";
        nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
        home-manager.url = "github:nix-community/home-manager/master";
        home-manager.inputs.nixpkgs.follows = "nixpkgs";
      };
    
      outputs = { self, nixpkgs, home-manager, ... }:
        let
          system = "x86_64-linux";
          lib = nixpkgs.lib;
          pkgs = nixpkgs.legacyPackages.${system};
        in {
        nixosConfigurations = {
          eva = lib.nixosSystem {
            inherit system;
	    modules = [ ./configuration.nix ];
          };
        };
        homeConfigurations = {
          asulk = home-manager.lib.homeManagerConfiguration {
            inherit pkgs;
	    modules = [ ./home.nix ];
          };
        };
      };
    }
