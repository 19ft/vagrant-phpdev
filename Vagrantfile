# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |c|

  c.vm.define "phpdev", primary: true do |config|

    # config.vm.box = "ubuntu/trusty64"
    config.vm.box = "19ft/phpdev"

    # config.vm.box_check_update = false

    config.vm.network "private_network", ip: "192.168.99.202"

    # Set hostname
    config.vm.hostname = "phpdev.localhost"
    if Vagrant.has_plugin?('vagrant-hostsupdater')
      config.hostsupdater.aliases = ["phpmyadmin.phpdev.localhost", "mailcatcher.phpdev.localhost", "profiler.phpdev.localhost"]
    end

    # Prevent Vagrant 1.7 from asking for the vagrant user's password
    config.ssh.insert_key = false

    # Provider-specific configuration so you can fine-tune various
    # backing providers for Vagrant. These expose provider-specific options.
    # Example for VirtualBox:
    #
    # config.vm.provider "virtualbox" do |vb|
    #   # Don't boot with headless mode
    #   vb.gui = true
    #
    #   # Use VBoxManage to customize the VM. For example to change memory:
    #   vb.customize ["modifyvm", :id, "--memory", "1024"]
    # end
    #

    # Start bash as a non-login shell & tell it to source /etc/profile
    # (Prevents "stdin: is not a tty error" warning)
    config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

    # Run ansible directly on guest
    config.vm.provision :shell,
      :keep_color => true,
      :inline => "export PYTHONUNBUFFERED=1 && export ANSIBLE_FORCE_COLOR=1 && cd /vagrant/vm-provisioning && ./init.sh"
    

  end
end
