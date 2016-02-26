# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/vivid64"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.define "icinga2-master" do |master|
    master.vm.hostname = "icinga2-master"
    master.vm.network :private_network, ip: "192.168.33.33"
    master.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/icinga2-master/playbook.yml"
      ansible.inventory_path = "provisioning/inventory"
      ansible.sudo = true
    end
  end

  config.vm.define "icinga2-remote" do |remote|
    remote.vm.hostname = "icinga2-remote"
    remote.vm.network :private_network, ip: "192.168.33.34"
    remote.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/icinga2-remote/playbook.yml"
      ansible.inventory_path = "provisioning/inventory"
      ansible.sudo = true
    end
  end
end
