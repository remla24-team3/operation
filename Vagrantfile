Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-24.04"
  config.vm.box_version = "202404.26.0"

  config.vm.define "controller" do |controller|
    controller.vm.hostname = "controller"
    controller.vm.network "private_network", ip: "192.168.56.2"
    
    controller.vm.provider "virtualbox" do |vb|
      vb.memory = "6144"
      vb.cpus = 2
    end

    config.vm.provider "vmware_fusion" do |v|
      v.vmx["memsize"] = "6144"
      v.vmx["numvcpus"] = "2"
    end

    controller.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/playbooks/k8s-setup.yml"
      ansible.inventory_path = "ansible/inventory.cfg"
      ansible.compatibility_mode = "2.0"
      ansible.groups = {
        "controller" => ["controller"]
      }
    end
  end

  (1..2).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname = "node#{i}"
      node.vm.network "private_network", ip: "192.168.56.#{i+2}"
      
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "6144"
        vb.cpus = 2
      end

      config.vm.provider "vmware_fusion" do |v|
        v.vmx["memsize"] = "6144"
        v.vmx["numvcpus"] = "2"
      end

      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbooks/k8s-setup.yml"
        ansible.inventory_path = "ansible/inventory.cfg"
        ansible.compatibility_mode = "2.0"
        ansible.groups = {
          "worker" => ["node#{i}"]
        }
      end
    end
  end
end
