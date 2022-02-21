# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "almalinux/8"
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.provider "libvirt" do |hv|
    hv.cpus = "2"
    hv.memory = "3072"
    # hv.storage :file, :size => "5G"
    # hv.storage :file, :size => "30G"
  end
  config.vm.define "nexus" do |nexus|
    nexus.vm.network "forwarded_port", guest: 443, host: 8443
    nexus.vm.network :private_network, ip: "192.168.3.10"
    nexus.vm.hostname = "nexus"
    nexus.vm.provision "ansible" do |a|
      a.verbose = "v"
      a.playbook = "deploy_nexus.yml"
    end
  end
end
