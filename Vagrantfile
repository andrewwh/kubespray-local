
# -*- mode: ruby -*-
# vi: set ft=ruby :

unless Vagrant.has_plugin?("vagrant-disksize")
    system "vagrant plugin install vagrant-disksize"
end

Vagrant.configure("2") do |config|
    # Common settings
    config.vm.box = "generic/ubuntu1804"
    config.vm.synced_folder "./", "/vagrant", type: "rsync", disabled: false
    config.ssh.insert_key = false
    # config.disksize.size = "20GB"

    # k8s-1
    config.vm.define "k8s-1" do |node|
        node.vm.network :private_network, ip: "172.17.8.101", dhcp_enabled: false
        node.vm.hostname = "k8s-1"
        node.vm.provision "shell", inline: "swapoff -a"

        node.vm.provider "virtualbox" do |v|
            v.name = "k8s-1"
            v.memory = 2048
            v.cpus = 1
            v.gui = false
            v.linked_clone = true
            v.customize ["modifyvm", :id, "--vram", "8"] # ubuntu defaults to 256 MB which is a waste of precious RAM
        end
    end

    # k8s-2
    config.vm.define "k8s-2" do |node|
        node.vm.network :private_network, ip: "172.17.8.102", dhcp_enabled: false
        node.vm.hostname = "k8s-2"
        node.vm.provision "shell", inline: "swapoff -a"

        node.vm.provider "virtualbox" do |v|
            v.name = "k8s-2"
            v.memory = 2048
            v.cpus = 1
            v.gui = false
            v.linked_clone = true
            v.customize ["modifyvm", :id, "--vram", "8"] # ubuntu defaults to 256 MB which is a waste of precious RAM
        end
    end    

    # k8s-3
    config.vm.define "k8s-3" do |node|
        node.vm.network :private_network, ip: "172.17.8.103", dhcp_enabled: false
        node.vm.hostname = "k8s-3"
        node.vm.provision "shell", inline: "swapoff -a"

        node.vm.provider "virtualbox" do |v|
            v.name = "k8s-3"
            v.memory = 2048
            v.cpus = 1
            v.gui = false
            v.linked_clone = true
            v.customize ["modifyvm", :id, "--vram", "8"] # ubuntu defaults to 256 MB which is a waste of precious RAM
        end
    end    
end