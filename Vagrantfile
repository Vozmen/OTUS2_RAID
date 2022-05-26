# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :linuxraid => {
        :box_name => "centos/7",
	:disks => {:sata1 => {
			:dfile => './sata1.vdi',
			:size => 250,
			:port => 1},

		       :sata2 => {
            :dfile => './sata2.vdi',
            :size => 250, # Megabytes
			:port => 2},

               :sata3 => {
            :dfile => './sata3.vdi',
            :size => 250,
            :port => 3},

               :sata4 => {
            :dfile => './sata4.vdi',
            :size => 250, # Megabytes
            :port => 4}
        }
    },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|

          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s
          #box.vbguest.installer_options = { allow_kernel_upgrade: true }
          #box.vm.network "forwarded_port", guest: 3260, host: 3260+offset

          box.vm.provider :virtualbox do |vb|
            	  vb.customize ["modifyvm", :id, "--memory", "1024"]
                  needsController = false
		  boxconfig[:disks].each do |dname, dconf|
			  unless File.exist?(dconf[:dfile])
				vb.customize ['createhd', '--filename', dconf[:dfile], '--variant', 'Fixed', '--size', dconf[:size]]
                                needsController =  true
                          end

		  end
                  if needsController == true
                     vb.customize ["storagectl", :id, "--name", "SATA", "--add", "sata" ]
                     boxconfig[:disks].each do |dname, dconf|
                         vb.customize ['storageattach', :id,  
                                      '--storagectl', 'SATA', '--port',
                                      dconf[:port], '--device', 0,
                                      '--type', 'hdd', '--medium', dconf[:dfile]]
                     end
                  end
          end
 	  box.vm.provision "shell", inline: <<-SHELL
            mkdir -p ~root/.ssh
            cp ~vagrant/.ssh/auth* ~root/.ssh
            mdadm --zero-superblock --force /dev/sd{b,c,d,e,f}
            yum install -y mdadm smartmontools hdparm gdisk
            mdadm --create --verbose --force /dev/md0 -l 4 -n 4 /dev/sd{b,c,d,e}
            sudo parted -s /dev/md0 mklabel gpt
            parted /dev/md0 mkpart "md01" ext4 0% 20%
            parted /dev/md0 mkpart "md02" ext4 20% 40%
            parted /dev/md0 mkpart "md03" ext4 40% 60%
            parted /dev/md0 mkpart "md04" ext4 60% 80%
            parted /dev/md0 mkpart "md05" ext4 80% 100%

  	  SHELL

      end
  end
end
	      

