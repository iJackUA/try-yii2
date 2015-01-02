# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

# check and install required Vagrant plugins
required_plugins = ["vagrant-hostmanager", "vagrant-vbguest", "vagrant-cachier"]
required_plugins.each do |plugin|
	if Vagrant.has_plugin?(plugin) then
	    system "echo OK: #{plugin} already installed"
	else
	    system "echo Not installed required plugin: #{plugin} ..."
		system "vagrant plugin install #{plugin}"
	end
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    # Every Vagrant virtual environment requires a box to build off of.
    config.vm.box = "Ubuntu14.04"

    # The url from where the 'config.vm.box' box will be fetched if it
    # doesn't already exist on the user's system.
    config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

    # Uncomment this line and remove config.vm.box_url above
    # if you need to use 32 bit of Ubuntu
    # config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-i386-vagrant-disk1.box"

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    config.vm.network "private_network", ip: "192.168.33.33"

    # Create a public network, which generally matched to bridged network.
    # Bridged networks make the machine appear as another physical device on
    # your network.
    # config.vm.network "public_network"

    # If true, then any SSH connections made will enable agent forwarding.
    # Default value: false
    # config.ssh.forward_agent = true

    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    config.vm.synced_folder "./", "/var/www"
    # Provider-specific configuration so you can fine-tune various
    # backing providers for Vagrant. These expose provider-specific options.
    # Example for VirtualBox:
    #
    config.vm.provider "virtualbox" do |vb|
        # Don't boot with headless mode
        # vb.gui = true
        # Use VBoxManage to customize the VM. For example to change memory:
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--name", "TryYii2"]
        vb.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "90"]
        # By default set to 1, change it to amount of your CPUs
        vb.customize ["modifyvm", :id, "--cpus", "2" ]
        # Or uncomment line above for Automatic set VirtualBox guest CPU count to the number of host cores
        # WARNING ! Works on Linux Host ONLY
        # vb.customize ["modifyvm", :id, "--cpus", `grep "^processor" /proc/cpuinfo | wc -l`.chomp ]
    end

    # Set entries in hosts file
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
    config.hostmanager.aliases =  ["yii2.local","admin.yii2.local","phpmyadmin.yii2.local","adminer.yii2.local"]

    if Vagrant.has_plugin?("vagrant-cachier")
        config.cache.scope = :box
    end

    #
    # Pre-provisioning
    # Install Ansible on the VM to run main provisioning from the VM itself
    #
    $script = <<SCRIPT
        sudo apt-add-repository ppa:rquillo/ansible -y
        sudo apt-get update -y
        sudo apt-get install ansible -y
SCRIPT

    config.vm.provision "shell", inline: $script

    #
    # Run Ansible provisioning inside the VM
    #
    config.vm.provision "shell" do |sh|
        sh.inline = "ansible-playbook /vagrant/provisioning/main.yml -i 'vagrant,' --connection=local"
    end
end
