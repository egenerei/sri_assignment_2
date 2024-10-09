# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  #server
  config.vm.define "server" do |dhcp|
    dhcp.vm.network  "private_network",
     ip: "192.168.56.10"
    dhcp.vm.network  "private_network",
      ip: "192.168.57.10",
      virtualbox__intnet: true
    #ojo al poner las rutas de la compartida, siempre /vagrant delante o no funciona
    dhcp.vm.provision "shell", inline: <<-script
      apt-get update
      apt-get upgrade -y
      apt-get install isc-dhcp-server -y
      cp -v /vagrant/shared/dhcp_settings/isc-dhcp-server /etc/default/ 
      cp -v /vagrant/shared/dhcp_settings/dhcpd.conf /etc/dhcp/
      systemctl restart isc-dhcp-server
      script
  end

  #client1
  config.vm.define "client1" do |cl1|
    cl1.vm.network  "private_network",
      type: "dhcp",
      virtualbox__intnet: true
  end
  #client2
  config.vm.define "client2" do |cl2|
    cl2.vm.network  "private_network",
      type: "dhcp",
      mac: "08002722edc6",
      virtualbox__intnet: true
  end
end