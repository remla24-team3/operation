# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  # controller node
  config.vm.define "controller" do |controller|
    controller.vm.box = "bento/ubuntu-24.04"
    controller.vm.box_version = "202404.26.0"
    controller.vm.network "private_network", ip:"192.168.57.2"
    controller.vm.provider "virtualbox" do |v|
      v.memory = 4096
      v.cpus = 1
    end

    controller.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "setup_ansible.yml"
      ansible.inventory_path = "inventory.yaml"
      ansible.groups = {
        "controllers" => ["controller"]
      }
    end

  end

  # node VMs
  (1..2).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "bento/ubuntu-24.04"
      node.vm.box_version = "202404.26.0"
      node.vm.network "private_network", ip:"192.168.57.#{i+2}"
      node.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 1
      end

      node.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "setup_ansible.yml"
        ansible.inventory_path = "inventory.yaml"
        ansible.groups = {
          "nodes" => ["node#{i}"]
        }
      end
    end
  end
end
