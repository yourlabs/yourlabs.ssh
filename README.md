yourlabs.ssh
============

Ansible/BigSudo role to secure an SSH server and add users.

This role is particularily important because it's default behaviour is to setup
the remote host for easy further ansible/bigsudo calls.

Perfect for being the first command to run against a fresh server

First touch of a server
-----------------------

For example with Online.Net (my favority host since 2005, best bandwidth that I
know of), I get a host ip with a user password and a root password and some OS
that I have choosen.

Before doing any Ansible job conveniently, the server needs to have my $USER
with my key (take it from github), sudo: ALL, forbid sshd password login, and
of course python but bigsudo deals with that last part by itself.

I will run this command:

    bigsudo yourlabs.ssh user@host --become --become-method=su --ask-become-pass

Other examples
--------------

Example usages:

    # configure ssh as sudo, will add a sudo group with passwordless sudo
    bigsudo yourlabs.ssh user@host -v --become

    # add a user with its github ssh keys
    bigsudo yourlabs.ssh user@host adduser username=jpic

    # add a user with a specific keys from a url
    bigsudo yourlabs.ssh user@host adduser username=jpic key=https://yourlabs.io/jpic.keys --become --ask-become-pass

Vagrant/VirtualBox
------------------

You can work in a VM if you have vagrant:

    cd yourlabs.ssh
    vagrant destroy -f && vagrant up
    vagrant ssh-config > ssh
    bigsudo . --ssh-common-args="-F ssh" @default --become -v
