# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  # machine_box = "xenial-server-cloudimg-amd64-vagrant"
  # machine_box_url = "https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"

  machine_box = "CentOS-7.1.1503-x86_64-netboot"

  config.vm.define "node44" do |machine|
    machine.vm.box = machine_box
    machine.vm.hostname = "node44"
    machine.vm.network "private_network", ip: "192.168.12.10"
    machine.vm.provider "virtualbox" do |node|
        node.name = "node44"
        node.memory = 1024
        node.cpus = 1
    end
   end


end
