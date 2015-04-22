# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "256"]
  end

  config.vm.define "naehfein" do |app|
    app.vm.hostname = "naehfein.dev"
    app.vm.box = "hashicorp/precise32"
    app.vm.network :private_network, ip: "192.168.60.4"
    app.vm.provision "shell",
                     inline: "sudo apt-get update"

    app.vm.provision "ansible" do |ansible|
      ansible.playbook = "naehfein.yml"
      ansible.inventory_path  = "inventories/naehfein_vagrant.cfg"
      ansible.limit = "all"

      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file:
          "~/.vagrant.d/insecure_private_key"
      }
    end
  end
end
