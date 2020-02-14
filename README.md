# vagrant-gravitational

## Why?

This is an as-code version of: https://gravitational.com/gravity/docs/quickstart/ using Vagrant, VirtualBox,
and the built-in Vagrant ansible-local provisioner.  I used the ansible-local provisioner so that this could be used
on any operating system supported by Vagrant since Ansible cannot be run on Windows as a controller.

The point of this was to learn how to use gravity and keep those notes in an as-code format for easy testing.

Note that this repo only gets you to the point of having the gravity control host and 3 deployment nodes ready 
for deployment.

**Hold up. Doesn't the gravitational quickstart already have a Vagrantfile?**

It does. That repo assumes you are running on Linux and have a bunch of tools installed on your
native Linux host.  This repo is designed to allow you to test gravity on Windows, Mac, or Linux
and does not require you to install anything on your native host.  It also installs everything
that is required for you.
  

## Installation

To run,

`vagrant up`

or if you are in a hurry and want to bring the hosts up in parallel ([which Vagrant does not support](https://www.vagrantup.com/docs/virtualbox/usage.html)):

`vagrant box add bento/ubuntu-18.04 || cat hostnames.txt | xargs -P4 -I {} vagrant up {}`

Note, the `vagrant box add bento/ubuntu-19.10` part of the above command only needs to be run
one time but it won't hurt to run it more than once.

This will take a while as it will pull down an ubuntu image, stand up 4 servers, update all of them,
install ansible, and then install everything needed for gravity.

Once this completes you will have a gravitational control server with all of the required components:

* docker
* git
* gravity
* helm

And you will have 3 empty nodes.

If you want to see the status of your boxes, use `vagrant status`:

```bash
~#: vagrant status                                                            1 ↵  1193  18:20:33
Current machine states:

gravity-control           running (virtualbox)
gravity-node0             running (virtualbox)
gravity-node1             running (virtualbox)
gravity-node2             running (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.

```

## Using the hosts

ssh into your control host: `vagrant ssh gravity-control`

Note, that you can reach your deployment nodes:

`ping gravity-node0.local`

This will get you ready to build your first gravity cluster:

https://gravitational.com/gravity/docs/quickstart/#building-a-cluster-image


## Cleanup

To shut down all the hosts, run

`vagrant halt`

To completely remove the hosts and their contents:

`vagrant destroy`

or if you don't want to be prompted before destroying each host:

`vagrant destroy -f`