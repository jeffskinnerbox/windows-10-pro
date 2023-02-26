# -*- mode: ruby -*-
# vi: set ft=ruby :

# Maintainer:   jeffskinnerbox@yahoo.com / www.jeffskinnerbox.me
# Version:      0.0.1


# Vagrantfile API/syntax version.  The "2" is the Vagrant configuration version.
VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.6.2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "baunegaard/win10pro-en"
    config.vm.box_version = "1.4.0"
    config.vm.communicator = "winrm"
    config.vm.hostname = "windows-10-pro.vm"   # set hostname

    # admin user name and password
    config.winrm.username = "vagrant"
    config.winrm.password = "vagrant"

    config.vm.guest = :windows
    config.windows.halt_timeout = 15

    config.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true

    # Share folder between the guest VM and the host.
    #    The first argument is the path on the host to the shared folder.
    #    The second argument is the path on the guest to mount the folder.
    #    And the remaining optional arguments not required.
    #config.vm.synced_folder "shared-data/", "/home/vagrant/shared-data", create: true, type: "virtualbox", :mount_options => ["dmode=777", "fmode=666"]
    #config.vm.synced_folder "/home/jeff/Documents/My Personal Files/My Finances/My Taxes/2022", "\\VBOXSVR\vagrant", create: true, type: "virtualbox", :mount_options => ["dmode=777", "fmode=666"]

    config.vm.provider :virtualbox do |v, override|
        v.gui = true
        #v.customize ["modifyvm", :id, "--memory", 4096]
        #v.customize ["modifyvm", :id, "--cpus", 2]
        v.customize ["modifyvm", :id, "--memory", 8192]
        v.customize ["modifyvm", :id, "--cpus", 4]
        v.customize ["modifyvm", :id, "--vram", 128]
        v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
        v.customize ["setextradata", "global", "GUI/SuppressMessages", "all"]
    end

    # add access to host optical drive
    config.vm.provider :virtualbox do |v, override|
        v.customize ["storageattach", :id, "--storagectl", "AHCI", "--port", "0", "--device", "0", "--type", "dvddrive", "--hotpluggable", "on", "--medium", "host:/dev/sr0"]
    end
end

