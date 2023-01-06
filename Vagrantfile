# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "ubuntu1" do |ubuntu1|
    ubuntu1.vm.box = "ubuntu/focal64"
    ubuntu1.vm.box_check_update = false
    ubuntu1.vm.hostname = "wordpress"
    ubuntu1.vm.network "private_network", ip: "192.168.100.10", nic_type: "virtio", virtualbox__intnet: "keepcoding"
    ubuntu1.vm.network "forwarded_port", guest: 80, host:8082
    ubuntu1.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
      vb.default_nic_type = "virtio"
      file_to_disk = "extradisk1.vmdk"
      unless File.exist?(file_to_disk)
        vb.customize [ "createmedium", "disk", "--filename", "extradisk1.vmdk", "--format", "vmdk", "--size", 1024 * 1 ]
    end
    vb.customize [ "storageattach", :id, "--storagectl", "SCSI", "--port", "1", "--device", "0", "--type", "hdd", "--medium", file_to_disk]
    end
  end

  config.vm.define "ubuntu2" do |ubuntu2|
    ubuntu2.vm.box = "ubuntu/focal64"
    ubuntu2.vm.box_check_update = false
    ubuntu2.vm.hostname = "elk"
    ubuntu2.vm.network "private_network", ip: "192.168.100.11", nic_type: "virtio", virtualbox__intnet: "keepcoding"
    ubuntu2.vm.network "forwarded_port", guest: 80
    ubuntu2.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
      vb.cpus = 1
      vb.default_nic_type = "virtio"
      file_to_disk = "extradisk2.vmdk"
      unless File.exist?(file_to_disk)
          vb.customize [ "createmedium", "disk", "--filename", "extradisk2.vmdk", "--format", "vmdk", "--size", 1024 * 1 ]
      end
      vb.customize [ "storageattach", :id, "--storagectl", "SCSI", "--port", "2", "--device", "0", "--type", "hdd", "--medium", file_to_disk]
    end
  end  
end