# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "Vozmen/centos-7-5"
#  config.vbguest.installer_options = { allow_kernel_upgrade: true }
  config.vm.network "public_network"
  config.ssh.forward_agent = true
  config.vm.provider "virtualbox" do |vb|
  config.vm.provider :virtualbox do |vb|
    vb.customize [
      "setextradata", :id,
      "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant-root", "1"
    ]
#     vb.customize [ 'storageattach', 
#        :id, # the id will be replaced (by vagrant) by the identifier of the actual machine
#        '--storagectl', 'IDE Controller', # one of `SATA Controller` or `SCSI Controller` or `IDE Controller`; 
#                                           # obtain the right name using: vboxmanage showvminfo  
#        '--port', 2,     # port of storage controller. Note that port #0 is for 1st hard disk, so start numbering from 1.
#        '--device', 0,   # the device number inside given port (usually is #0) 
#        '--type', 'hdd', 
#        '--medium', File.absolute_path('/home/vozmen/OTUS2_RAID/disk-2.vdi')] # path to our VDI image
    vb.customize [
      'modifyvm', :id,
      '--natdnshostresolver1', 'on',
      '--memory', '512',
      '--cpus', '2'
    ]
    end
  end
end
