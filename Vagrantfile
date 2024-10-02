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
    dhcp.vm.provision "shell", inline: <<-script
      sudo apt install isc-dhcp-server -y
      script
  end
  
end