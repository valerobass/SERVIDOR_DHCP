# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box_check_update = false
  config.vm.provision "shell", inline: <<-SHELL
  apt-get update
  apt-get install -y
 SHELL

  config.vm.define :servidor do |servidor|
    servidor.vm.box = "debian/bookworm64"
    servidor.vm.hostname = "Servidor"
    servidor.vm.network "public_network",ip : "192.168.56.10"
    servidor.vm.network "private_network", ip: "192.168.57.10",
    virtualbox__intnet: true
    servidor.vm.provision "shell", inline: <<-SHELL
      apt-get isc-dhcp-server -y
    SHELL
  end

  config.vm.define :cliente1 do |c1|
    c1.vm.box = "debian/bookworm64"
    c1.vm.hostname = "cliente1"
    c1.vm.network "private_network", type: "dhcp",
      virtualbox__intnet: true
  end

  config.vm.define :cliente2 do |c2|
    c2.vm.box = "debian/bookworm64"
    c2.vm.hostname = "cliente2"
    c2.vm.network "private_network", type: "dhcp",
      virtualbox__intnet: true
  end
end

 

