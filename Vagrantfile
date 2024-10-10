# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|


  config.vm.define :servidor do |servidor|
    servidor.vm.box = "debian/bookworm64"
    servidor.vm.hostname = "Servidor"
    servidor.vm.network "private_network",ip: "192.168.56.10"
    servidor.vm.network "private_network", ip: "192.168.57.10",
    virtualbox__intnet: true
    servidor.vm.provision "shell", inline: <<-SHELL
      apt-get update 
      apt-get install -y isc-dhcp-server 
      cp -v /vagrant/isc-dhcp-server /etc/default/isc-dhcp-server
      cp -v /vagrant/dhcp.conf /etc/dhcp/dhcpd.conf
      systemctl restart isc-dhcp-server
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
    c2.vm.network "private_network",
      mac: "5CA1AB1E0001",
      auto_config: false,
      virtualbox__intnet: true
    c2.vm.provision "shell", inline: "dhclient eth1"
  end
end

 

