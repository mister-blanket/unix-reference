# Bash Reference

<!-- TOC -->
- [File System](#file-system)
  - [Encryption](#encryption)
    - [Encrypting external drives](#encrypting-external-drives)
  - [Making Bootable USB](#making-bootable-usb)
  - [Mounting iPhone](#mounting-iphone)
    - [iFuse](#ifuse)
- [Document Editing](#document-editing)
  - [MarkDown](#markdown)
    - [TOC](#toc)
  - [PDF Creation](#pdf-creation)
    - [img2pdf](#img2pdf)

<!-- TOC END -->


## File System


### Encryption

#### Encrypting external drives
https://averagelinuxuser.com/encrypt-hard-drive-in-linux/
This will wipe the entire drive.

__Encrypting__
* Use Gparted (GUI) to check device. If you want to encrypt the entire drive, only one partition is needed.
* Use `df` or `lsblk` to confirm the desired partition.
* Unmount device: `sudo umount /dev/sd*1`
* Encrypt partition: `sudo cryptsetup --verbose --verify-passphrase luksFormat /dev/sd*1`
* Open partition: `sudo cryptsetup luksOpen /dev/sd*1 sd*1`
* Check where disk is mapped: `sudo fdisk -l`, probably `/dev/mapper/sd*1`
* Make a filesystem: `sudo mkfs.ext4 /dev/mapper/sd*1`

__Testing__
* Mount: `sudo mount /dev/mapper/sdb1 /mnt`
* Add yourself as owner of drive: `sudo chown -R michael /mnt`
* Add files to drive: `sudo touch /mnt/test.txt`
* Unmount: `sudo umount /dev/mapper/sd*1`
* Close device: `sudo cryptsetup luksClose sd*1`

__Usage__
* Decrypt: `sudo cryptsetup luksOpen /dev/sd*1 sd*1`
* Mount: `sudo mount /dev/mapper/sd*1 /mnt`
* Manage files
* Unmount: `sudo umount /dev/mapper/sd*1`
* Close device: `sudo cryptsetup luksClose sd*1`




### Making Bootable USB

Burn ISO to disk: `sudo dd bs=4M if=/path/to/iso of=/dev/sdX status=progress && sync`

Clean flash drive: `sudo wipefs --all /dev/sdX`

Create a new partition: `sudo cfdisk /dev/sdX`

Format this partition as FAT file system: `sudo mkfs.vfat -n 'yourlabel' /dev/sdX1`


### Mounting iPhone


#### iFuse

`ifuse ~/Pictures/iphone`


## Document Editing


### MarkDown


#### TOC

Table of contents creator.  
Add `<!-- TOC -->` in MarkDown file where you want the TOC to go.   
Then `toc-md /path/to/markdown`


### PDF Creation


#### img2pdf
`img2pdf img1.png img2.jpg -o out.pdf`
