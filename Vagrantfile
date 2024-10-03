# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.vm.provision "shell", inline: <<-script
      apt update
      apt upgrade -y
    script
  #server
  config.vm.define "server" do |dhcp|
    dhcp.vm.network  "private_network",
     ip: "192.168.56.10"
    dhcp.vm.network  "private_network",
      ip: "192.168.57.10",
      virtualbox__intnet: true
    #ojo al poner las rutas de la compartida, siempre /vagrant delante o no funciona
    dhcp.vm.provision "shell", inline: <<-script
      apt install isc-dhcp-server -y
      cp -v /vagrant/shared/dhcp_settings/isc-dhcp-server /etc/default/ 
      cp -v /vagrant/shared/dhcp_settings/dhcpd.conf  /etc/dhcp/
      script
  end
  #client
  config.vm.define "client" do |cl|
    cl.vm.network  "private_network",
      type: "dhcp",
      virtualbox__intnet: true
  end
end