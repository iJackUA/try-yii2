# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    # All Vagrant configuration is done here. The most common configuration
    # options are documented and commented below. For a complete reference,
    # please see the online documentation at vagrantup.com.

    # Every Vagrant virtual environment requires a box to build off of.
    config.vm.box = "Ubuntu14.04"

    # The url from where the 'config.vm.box' box will be fetched if it
    # doesn't already exist on the user's system.
    config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

    # Disable automatic box update checking. If you disable this, then
    # boxes will only be checked for updates when the user runs
    # `vagrant box outdated`. This is not recommended.
    # config.vm.box_check_update = false

    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine. In the example below,
    # accessing "localhost:8080" will access port 80 on the guest machine.
    # config.vm.network "forwarded_port", guest: 80, host: 8080

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
        # vb.customize ["modifyvm", :id, "--cpus", "1" ]
        # Or uncomment line above for Automatic set VirtualBox guest CPU count to the number of host cores
        # WARNING ! Works on Linux Host ONLY
         vb.customize ["modifyvm", :id, "--cpus", `grep "^processor" /proc/cpuinfo | wc -l`.chomp ]
    end

    # Set entries in hosts file
    # https://github.com/cogitatio/vagrant-hostsupdater
    if Vagrant.has_plugin?("vagrant-hostsupdater")
        config.hostsupdater.remove_on_suspend = true
        config.vm.hostname = "yii2.local"
        config.hostsupdater.aliases = ["admin.yii2.local","phpmyadmin.yii2.local"]
    end

    if Vagrant.has_plugin?("vagrant-cachier")
        config.cache.scope = :box
    end

    # Ansible provisioning (you can use this or Shell)
    # To use Ansible provisioning you should habe Ansible installed on your host machine
    # see here http://docs.ansible.com/intro_installation.html#installing-the-control-machine
    config.vm.provision "ansible" do |ansible|
        # should be equal to host name in Ansible hosts file
        ansible.limit = "vagrant"
        ansible.playbook = "provisioning/main.yml"
        ansible.inventory_path = "provisioning/hosts"
        # set to 'vvvv' for debug output in case of problems
        ansible.verbose = false
        ansible.host_key_checking = false
    end
end
