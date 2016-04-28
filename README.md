# CentOS
How to Create Bootable USB for Custom Centos 6.6 with Text mode and kickstart config

mount -t iso9660 -o loop /tmp/centos6.6.iso /mnt/centos/
cd /tmp/build/
cp -r /mnt/centos/ .
#do some change here and then re-create iso files
mkisofs -r -R -J -T -quiet -no-emul-boot -boot-load-size 4 -boot-info-table -V "New-CentOS" -sparc-label "New-CentOS" -p "zhanyh@outlook.com" -A "New Centos YHTEST1" -b isolinux/isolinux.bin -c isolinux/boot.cat -x "lost+found" -o /tmp/new_centos_rc1.iso /tmp/build/centos/
# don't forget this otherwise your USB is not bootable
isohybrid.pl /tmp/new_centos_rc1.iso
implantisomd5 --supported-iso /tmp/new_centos_rc1.iso

After the custom iso created, you can create bootable USB disk.

You can use dd on Linux OS or Win32DiskImager with Windows OS
dd if=/tmp/new_centos_rc1.iso of=/dev/sdb 
Please use 'fdisk -l' to check your USB disk.

And then you can use the USB to install your custom centos OS.

If your hardware server doesn't support graphics (don't have monitor, no keyboard, no mouse ...), you may need to do following chagnes:
1. change isolinux.cfg
2. change ks.cfg

Please refer to those two files FYI.
