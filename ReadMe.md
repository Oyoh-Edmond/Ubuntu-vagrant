# Set up an Ubuntu virtual machine using Vagrant


 1. Install Vagrant:

    - If you haven't already installed Vagrant, download and install it from the official website: [Vagrant Downloads](https://www.vagrantup.com/).

2. Create a New Directory:

    - Create a new directory where you want to store your Vagrant project.

3. Initialize Vagrant:

   - Open a terminal or command prompt and navigate to the directory you just created. Then, run the following command to initialize a new Vagrant environment:
   ```#
   vagrant init
   ```

4. Download Ubuntu Box:

    - Once Vagrant is initialized, you need to add an Ubuntu box. Run the following command to add the Ubuntu 20.04 LTS (Focal Fossa) box:

    ```
    vagrant box add ubuntu/focal64
    ```
5. Open the Vagrantfile in a text editor. This file controls the configuration of your Vagrant environment. Customize it according to your needs. Here's an example:

    ```
    Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048" # Change this value based on your choice
        vb.cpus = 1        # Allocate at least 1 CPU core
    end

    # Configure networking
    config.vm.network "private_network", type: "dhcp"

    # Choose appropriate settings for display
    config.vm.provider "virtualbox" do |vb|
        vb.gui = true
        vb.customize ["modifyvm", :id, "--vram", "128"]
    end
    end
    ```

    ___This configuration sets up a Ubuntu 20.04 LTS virtual machine with 2048MB of RAM, 1 CPU core, NAT networking, and GUI display.___


6. Start the Virtual Machine:

    - Save the Vagrantfile and close the text editor. Then, run the following command on your terminal to start the virtual machine:

        ```
        vagrant up
        ```
7. Access the Virtual Machine:

    - Once the virtual machine is up and running, you can access it via SSH using the following command:

        ```
        vagrant ssh
        Login: vagrant
        password: vagrant
        ```


8. Install Ubuntu on the Virtual Machine:

    -  Ubuntu installation is typically handled automatically by the Vagrant box. You don't need to perform a manual installation.



# Setting up specific configurations to install python.

1. Create a shell script file in the same directory as your Vagrantfile. This script will contain the commands to install the desired packages.

2. Add the necessary commands to install Python and any other packages you want. Here's an example of how you can install Python:

     ```
    #!/bin/bash

    # Update package list
    sudo apt update

    # Install Python
    sudo apt install -y python3 python3-pip

    ```

3. Modify your Vagrantfile to include the provisioning script. Add the following line at the end of your Vagrantfile:

    ```
    config.vm.provision "shell", path: "installationpy.sh"
    ```
    ___This line tells Vagrant to run the shell script (installationpy.sh) during the provisioning process.___

4. Save your changes to the Vagrantfile.

5. Now, when you run vagrant up to create or start your virtual machine, Vagrant will automatically execute the provisioning script, installing Python and any other specified packages.
