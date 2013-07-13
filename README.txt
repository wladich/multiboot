multiboot
=========
1. Partitions setup:
    16 Mb for multiboot data and fake loader installations for linux
    /sbin/sfdisk /dev/sdX -uS < partitions.dump

make other parttions for LVM, Windows, etc

2. Make file system:
    mkfs.ext /dev/sdX2

4. mount multiboot data partio
    mkdir /mnt/multiboot
    mount /dev/sdX2 /mnt/multiboot

5. clone this repo:
    cd /mnt/multiboot
    git clone git@github.com:wladich/multiboot.git

6. Configure multiboot
Find boot disk id:
    ls -l /dev/sdX
And put it in /mnt/multiboot/etc/multiboot.cfg:
    boot_disk_id=XXXXXXXXXXXXXXXXXX
Add any modules required to load next stage
    add_modules="mod1 mod2 mod3"

7. Configure grub menu entries
   vim /mnt/multiboot/etc/grub.d/40_custom

8. Build and install loader
    cd /mnt/multiboot/bin
    ./update-grub-multiboot
    ./grub-install-multiboot