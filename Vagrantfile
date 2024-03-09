# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/focal64"
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "2048" # Change this value based on your choice
      vb.cpus = 1        # Allocate at least 1 CPU core
    end
  
    # Configure networking
    config.vm.network "private_network", ip: "192.168.50.10"
  
    # Choose appropriate settings for display
    config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--vram", "128"]
    end
  
    Vagrant.configure("2") do |config|
      # Other Vagrant configuration settings
    
      config.vm.provision "shell", path: "installationpy.sh"
    end

end
