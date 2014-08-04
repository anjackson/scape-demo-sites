# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    # Use the precised64 box, change this for 32 bit, or other distro
    config.vm.box = "hashicorp/precise64"

    # Set the box host-name
    config.vm.hostname = "scape-demos.hostname"

    #The permissions are messed up for the apache server user, fix here
    config.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=755", "fmode=755"]


    # Run the provisioning script	
    config.vm.provision :shell, :path => "./provision/bootstrap.sh"

    # Port forward HTTP (80) to host 2020
    config.vm.network :forwarded_port, :host => 2020, :guest => 80


    config.vm.provider :virtualbox do |vb|
      vb.name = "scape-demos-dev"
      vb.memory = 1024
      vb.cpus = 1
    end

    #These network things are nessesary to make ubuntu work fast
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
    config.vm.network :public_network, :nictype => 'virtio', :type => "dhcp", :use_dhcp_assigned_default_route => true

end
