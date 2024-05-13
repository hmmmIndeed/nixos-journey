# Nixos Journey

## Background Info

I have used NixOS once before during the school year, but only for around a week, so I never was able to properly use it. I'm going to document my journey using NixOS here since the documentation isn't the best and it's kinda confusing watching videos that don't really build off each other. The reason why it's hard to follow videos that don't build off each other is that they often use different things and are set up differently, such as some use home manager or flakes, others don't.

Also, I want to look back over what I've done on my system in case I have no idea what I previously did; it'll help me understand my previous saves. This is public so hopefully it'll help someone as confused as I am.

### Note

I am dual booting NixOS with Windows on two SSD's and am using a data partition so both operating systems can access some of the same files. 

How I'm setting my laptop up:

256 GB SSD:
* Windows

512 GB SSD:
* NixOS
* data partition

Also, I'm using a Thinkpad E14 Gen 4 which I have wiped multiple times to use Windows and NixOS (it's a long story) so I'm treating my laptop as if I'm installing on a new system with no data (so make sure to back up your data).

## Installing Windows

(When I say Linux, it means any Linux OS, including NixOS)

Since Windows can only be installed on an entire SSD, not on a drive partition, Windows should be installed first (it might not matter if it's on its own SSD such as with my case but it's better to be on the safe side and install Windows before Linux) (if Windows and Linux are to be installed on the same SSD, Windows MUST be installed first).

