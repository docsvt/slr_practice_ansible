# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.provider "libvirt" do |libvirt|
    # Customize the amount of memory on the VM:
    libvirt.memory = "4096"
  end
  
  config.vm.box_check_update = false
  config.vm.define "pnode" do |pnode|
    pnode.vm.box = "centos/7"
    pnode.vm.hostname = "pnode"
    pnode.vm.network "forwarded_port", guest: 80, host: 8080
    pnode.vm.network "private_network", ip: "192.168.50.5"
    pnode.vm.box_check_update = false
    pnode.vm.provision "shell", inline: <<-SHELL
      sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/#g' /etc/ssh/sshd_config
      sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/#g' /etc/ssh/sshd_config       
      systemctl restart sshd
    SHELL
  end
  
end
