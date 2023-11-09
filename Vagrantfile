# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_INSTANCE_NAME = "devbox"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.box_check_update = false
  config.vm.define VAGRANT_INSTANCE_NAME
  config.vm.hostname = VAGRANT_INSTANCE_NAME

  config.vm.provision "file", source: "~/.ssh", destination: "/tmp/ssh_config"
  config.vm.provision "file", source: "scripts/playbook.yml", destination: "/tmp/playbook.yml"
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.provisioning_path = "/tmp"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.name = VAGRANT_INSTANCE_NAME
    vb.memory = 2048
  end
  config.vm.disk :disk, size: "100GB", primary: true
end

