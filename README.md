# OTUS
HomeWork2
  config.vbguest.installer_options = { allow_kernel_upgrade: true } убирает ошибку 

The following SSH command responded with a non-zero exit status.
Vagrant assumes that this means the command failed!

umount /mnt

Stdout from the command:



Stderr from the command:

umount: /mnt: not mounted




cd /opt/VBoxGuestAdditions-*/init  
sudo ./vboxadd setup

vagrant plugin uninstall vagrant-vbguest
vagrant plugin install vagrant-vbguest
