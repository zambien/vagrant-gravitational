# vagrant-gravitational

This is an as-code version of: https://gravitational.com/gravity/docs/quickstart/ using Vagrant, VirtualBox,
and the built-in Vagrant ansible-local provisioner.  I used the ansible-local provisioner so that this could be used
on any operating system supported by Vagrant since Ansible cannot be run on Windows as a controller.

The point of this was to learn how to use gravity and keep those notes in an as-code format for easy testing.

Note that this only gets you to the point of having the gravity control ost ready for deployment.  To run,

`vagrant up`

Once this completes you will have a gravitational control server with all of the required components:

* docker
* git
* gravity
* helm

This will get you to this point currently:

https://gravitational.com/gravity/docs/quickstart/#building-a-cluster-image