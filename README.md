<!--
Maintainer:   jeffskinnerbox@yahoo.com / www.jeffskinnerbox.me
Version:      0.0.1
-->


<!--
<div align="center">
<img src="http://www.foxbyrd.com/wp-content/uploads/2018/02/file-4.jpg" title="These materials require additional work and are not ready for general use." align="center">
</div>


-----
-->


# Windows 10 Pro on Linux
With few exceptions, I have abandon MicroSoft Windows OS for Linux.
I do fined an occasional need for MS Windows for some odd MS Windows program I may wish to run,
but the only constant need is filing my annual income tax using TurboTax.
When it comes to Linux,
you have a few options to consider to fill in for the Windows program void.
The specific options I explored for TurboTax tax filing:

1. **Native Linux -**
In some cases, you can find Linux programs that claim some equivalency to the MS Windows version.
There happens to be at least one such package for filling taxes.
    * [Use Linux to do your taxes][01]
1. **Bottles / Wine -**
Wine is a compatibility layer capable of running Windows applications on Linux.
Instead of simulating internal Windows logic like a virtual machine or emulator,
Wine translates Windows API calls into Linux calls on-the-fly.
Bottles is a wrapper around Wine, simplifying and automating some task.
    * [How to Run Windows Software on Linux With Bottles][02]
1. **Proxmox -**
Proxmox is an open-source, Type 1 hypervisor that comes as a Debian-based Linux distribution.
With Proxmox, users can experience a hypervisor that can integrate Linux containers (LXC),
KVM hypervisor virtual machines, networking functionality, and software-defined storage in a unified platform.
([Windows 10 downloads required][03]).
    * [Installing ProxMox and Installing Windows as Virtual Machine in ProxMox (2022 Guide)][04]
    * [HowTo install & configure Windows 10 in a VM on Proxmox VE 7.1 - step-by-step][08]
1. **Vagrant/VirtualBox -**
Oracle VM VirtualBox is a type-2 hypervisor for x86 virtualization package
supporting a large number of guest operating systems.
Vagrant is a wrapper around VirtualBox that provides some portability across many
hypervisors like VirtualBox, KVM, Hyper-V, VMware, etc.
Pre-built VM are provided, including for MicoSoft Windows
(e.g. [gusztavvargadr/windows-10][05]).
    * [How to Install Windows 10 in a Virtual Machine][06]

The solutions Proxmox and Vagrant/VituralBox worked well for me,
and I settled in on using the later.

>**NOTE:** Beware of the "Guru Meditation" error.
>This is a VirtualBox error that I got, and in my case, it was cause by a incompatibility
>between VirtualBox and KVM.
>The solution was to remove KVM, or at least stop its operations temporarily.
>See "[Virtualbox Guru Meditation Critical Error In Linux][07]".


----


# Windows 10 Pro VM
Now that multiple Vagrant boxes are available for Windows 10
(e.g. Vagrant Cloud repository [`baunegaard/win10pro-en`][09]),
I have no need to build my own Vagrant box.
This Vagrant box is setup such that it can share the directory in which the `vagrant` command is executed.
This is great so I can write/read any files I need via this shared directory.

My plan is to load this Windows 11 VM with TurboTax and file my taxes.
My TurboTax is on a CD-ROM, therefore I want to load that software directly from the CD.
To do this, I need the CD/DVD optical reader on my host computer to share with the MS Windows 10 guest VM.

## Creating the Windows 10 VM Vagrantfile
Using the Vagrant base box [`baunegaard/win10pro-en`][09],
I need to create a Vagrantfile to meet my needs stated above.
To derive the Vagrantfile,
I experimented with provisioning VirtualBox directly using [VBoxManage][10]
and leveraged the learnings from [jeffskinnerbox / Windows-10-Vagrant-Box][11].

Sources used to understand what was needed:

* [Create VirtualBox VM from the command line](http://www.perkin.org.uk/posts/create-virtualbox-vm-from-the-command-line.html)
* [Vagrant - Adding a second hard drive](https://everythingshouldbevirtual.com/virtualization/vagrant-adding-a-second-hard-drive/)
* [Add an empty optical drive to Oracle VirtualBox instance with the Vagrantfile](https://medium.com/@njeremymiller/add-an-empty-optical-drive-to-oracle-virtualbox-instance-with-the-vagrantfile-523e8e9114be)
* [How to add storage settings to Vagrant file?](https://stackoverflow.com/questions/21986511/how-to-add-storage-settings-to-vagrant-file)
* [FIX FOR VBOXMANAGE: ERROR: COULD NOT FIND A CONTROLLER NAMED ‘SATA’ ERROR](https://www.minvolai.com/fix-for-vboxmanage-error-could-not-find-a-controller-named-sata-error/)



[01]:https://opensource.com/article/21/2/linux-tax-software
[02]:https://www.makeuseof.com/run-windows-apps-on-linux-with-bottles/
[03]:https://www.microsoft.com/en-us/software-download/windows10ISO
[04]:https://www.youtube.com/watch?v=lwORpWEHiDE
[05]:https://app.vagrantup.com/gusztavvargadr/boxes/windows-10
[06]:https://www.extremetech.com/computing/198427-how-to-install-windows-10-in-a-virtual-machine
[07]:https://ostechnix.com/virtualbox-guru-meditation-critical-error-in-linux/
[08]:https://blog.habitats.tech/howto-install-and-configure-windows-10-in-a-vm-on-proxmox-ve-71-step-by-step
[09]:https://app.vagrantup.com/baunegaard/boxes/win10pro-en/versions/1.4.0
[10]:https://docs.oracle.com/cd/E97728_01/E97727/html/vboxmanage-intro.html
[11]:https://github.com/jeffskinnerbox/Windows-10-Vagrant-Box

