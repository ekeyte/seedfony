# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# windows test
def which(cmd)
    exts = ENV["PATHEXT"] ? ENV["PATHEXT"].split(";") : [""]
    ENV["PATH"].split(File::PATH_SEPARATOR).each do |path|
        exts.each { |ext|
            exe = File.join(path, "#{cmd}#{ext}")
            return exe if File.executable? exe
        }
    end
    return nil
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Hostname
  config.vm.hostname = "ansible.vm"

  # Base Box
  config.vm.box = "ubuntu/trusty64"

  # Network Forwarded port.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Private Network ID.
  config.vm.network "private_network", ip: "172.16.0.16"

  # Synced Folders (Mounted)
  config.vm.synced_folder "seedfony", "/var/www/seedfony"

  config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     vb.gui = false

     # Customize the amount of memory (mb) on the VM:
     vb.memory = "1024"
  end

  # Use Ansible to provision.
  config.vm.provision "ansible" do |ansible|
     ansible.limit = "all"
     ansible.verbose = "v"
     ansible.inventory_path = "provisioning/inventory/inventory.yml"
     ansible.playbook = "provisioning/playbook.yml"
     ansible.extra_vars = { ansible_ssh_user: 'vagrant', app_env: 'local', nginx_user: 'vagrant' }
  end
end
