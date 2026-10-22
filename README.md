## FEDInstall (pre-LARBS)
This script installs encrypted base Artix Linux system. No feds attached!

### Why?
Because I want all my systems to be encrypted, but I'm lazy and I hate
configuring it all by hand. Also, existing install scripts either don't install
true FDE, which is a shame, or don't provide such flexibility with
encryption/drive setup options, or are very unintuitively written. This script
aims to set up the best possible encryption, while still being very easy to
use.

## Features
* Works for both legacy boot and UEFI systems.
* Optional LVM - separate /root and /home logical volumes
* Full Disk Encryption using LUKS:
	* For legacy boot, the drive is 100% encrypted.
	* For EFI systems a separate unencrypted partition for EFI files is
	  created.
* Keyfile is used so there's no need to enter the decryption password twice.
* Speeds up boot by reducing grub timeout.
* Perfect to run before LARBS!

## Usage
You can run the script from live Artix ISO. You can also run it from an already
installed system, if you install `artools-base` package.

### Basic usage:
Just give the script a drive to install the system on and a password for it.
**Be careful to not choose the wrong drive, as the script will erase it!**

```
fedinstall -d </dev/path-to-drive> -p <password-for-decryption>
```

If you don't like the password appearing in the history, don't pass -p flag and
the script will prompt you for the password.

### Options:

```
  -d  drive to install on (e.g. /dev/sdX, /dev/nvme...)
  -f  file system for the root partition (ext4, btrfs etc)
  -h  hostname
  -l  set up LVM /root and /home logical volumes
  -n  name for the encrypted system partition
  -p  password for system decryption
  -t  time zone (file in /usr/share/zoneinfo/, e.g. Europe/Kyiv)
  -v  be verbose"
```

## After install
When the script is done, you should have a completely functioning base Artix
system. You can set up users and graphical environment by yourself, or (better)
use [LARBS](https://larbs.xyz) or some other script for that.

## TODO
- [ ] Write a version which will set up a system to be bootable from both
      legacy boot and UEFI.
- [ ] Make script detect the distro running (Arch/Artix) and modify commands
      accordingly
- [ ] (maybe) create an option for legacy boot with separate, unencrypted,
      /boot partition?
