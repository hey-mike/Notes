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
