## Clean vagrant build
vagrant global-status --prune - Prunes invalid entries from the list. This is much more time consuming than simply listing the entries.

# c;i


# Set vagrant up default box
By passing `primary` flag to the the machine definition to start the machine as default machine when passing `vigrant up`
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"
    Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
        config.vm.define "web", primary: true do |web|
        web.vm.box ="puppetlabs/ubuntu-14.04-32-nocm"
    end
end
```
We'll need to install a service that will run on port 80 of the guest machine. To do
this, we'll add a simple provisioning command. The complete Vagrantfile now looks
like this:

```ruby
web.vm.provision "shell", inline: "apt-get install -y nginx"
```

With the auto_correct option, Vagrant will first attempt to connect to the specified
port (in this example, 8888), then fail over to a different port if the one specified is being
used by another process.
```ruby
web.vm.network "forwarded_port", guest:80, host:8888, auto_correct: true
```


To enable the GUI, we will need to add a provider-specific block to the configuration.
In this case, the provider is "virtualbox".
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "chad-thompson/ubuntu-trusty64-gui" config.
    vm.provider "virtualbox" do |vbox|
        vbox.gui = true
    end
end
```

synced_folder
```ruby
web.vm.synced_folder "vagrantsite/", "/opt/vagrantsite"
```
This will link the `vagrantsite` directory we created in step 1 to the `/opt/vagrantsite` directory on the guest machine.


# Ansible - is designed to execute commands using SSH
currently it is not supporting Windows

installlation: 
```bash
sudo pip install ansible
```
or for mac
```bash
brew install ansible
```


# Vagrant newtwork 
```ruby
config.vm.network "private_network", ip: "192.168.99.100"
```
Add ``web.local 192.168.99.100`` to  ``/etc/hosts``, The Vagrant machine can then be accessed using the ``web.local`` name address rather than a forwarded port address of something like ``http://localhost:8080``

## Multiple machines
The ordering and overriding of provisioners and variables is especially important in
multimachine Vagrant environments. A multimachine Vagrantfile can specify global
parameters (such as boxes or common provisioning tasks) that allow for individual
machines to override the global parameters
