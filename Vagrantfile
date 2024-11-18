# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

    config.vm.define "docker-box" do |vm1|
      config.ssh.private_key_path = "/home/apollo/TST-VBOX/.ssh/id_rsa"
      config.ssh.forward_agent = true
      config.ssh.username = "vagrant"
      config.ssh.password = "vagrant"
      vm1.vm.hostname = "docker-box"
      vm1.vm.box = "bento/ubuntu-22.04"
      vm1.vm.network "public_network", auto_config: false
      # vm1.vm.network "forwarded_port", guest: 8200, host: 8200
      vm1.vm.synced_folder ".", "/home/vagrant/"
      vm1.vm.provider "virtualbox" do |vb|
        vb.name = "docker-box"
        vb.memory = "8192"
        vb.cpus = 4
        vb.gui = false
      end
  
      vm1.vm.provision "shell", run: "always", inline: <<-SHELL
        sudo apt-get update
        sudo apt-get install net-tools zip curl jq tree unzip wget siege apt-transport-https ca-certificates software-properties-common gnupg lsb-release -y
        netstat -tunlp
        ifconfig eth1 10.4.1.155 netmask 255.255.255.0 up
        route add default gw 10.4.1.254
      SHELL
  
      vm1.vm.provision "shell",
        privileged: true,
        path: './scripts/1-docker-install.sh'
  
      end
  end