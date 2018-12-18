# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  default_shared_folder = "#{ENV.fetch('HOME')}/workspace"
  shared_folder = ENV.fetch('LINUX_PLAYGROUND_SHARED_DIR', default_shared_folder)
  config.vm.synced_folder shared_folder, "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    vb.name = 'linux-playground'

    require 'etc'
    num_cpus = Etc.nprocessors
    vb.cpus = ENV.fetch('LINUX_PLAYGROUND_CPUS', num_cpus)

    vb.memory = ENV.fetch('LINUX_PLAYGROUND_MEMORY', 2048)
  end

  config.vm.provision "shell" do |s|
    s.inline = "sudo apt update && sudo apt install -y python-dev"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
