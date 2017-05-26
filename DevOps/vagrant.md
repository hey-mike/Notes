## Clean vagrant build
vagrant global-status --prune - Prunes invalid entries from the list. This is much more time consuming than simply listing the entries.


## Common issue when integrate with docker as provider
1. docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.26/containers/create: dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.

Solution: 
1. sudo usermod -a -G docker $USER
2. completely log out of your account and log back in


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
