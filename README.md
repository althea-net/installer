# Althea Installer

This is the installer for Althea on general purpose Linux. Whereas the [Althea
firmware](https://github.com/althea-mesh/althea-firmware) which is targeted at
OpenWRT compatible routers this installer will work on normal deskop and server
Linux distributions.

Eventually we will publish more traditional packages, right now this takes binaries
that you build and sets them up on a remote machine. 

----------------

Is this where I get Althea?
------------------------------------------

If you just want Althea on your computer please download a release from
our website once it becomes available. This page is for developers who want
to help improve Althea. Or technically advanced users who want to try out cutting
edge changes.

Getting Started
--------------------

First off you need a Linux machine with Ansible.

On Ubuntu and Debian:
> sudo apt install python-pip libsqlite3-dev libssl-dev build-essential

> sudo pip install ansible

On Fedora:
> sudo dnf install ansible sqllite3-devel openssl-devel gcc

On Centos and RHEL:
> sudo yum install ansible sqllite3-devel openssl-devel gcc

All other required software will be installed by the setup playbook

Setting up an Exit server
-------------------------

An Althea Exit server is essentially a WireGuard proxy server setup to integrate
with the mesh network.

Create a file named `hosts` and populate it with the ip addreses
of your exit server like so.

>[exit]
>server a
>server b

You can then put some sort of load balancer in front of multiple servers. Optionally
of course.

Profiles are variables files pulled into Ansible for easy customization of what
the playbook will do. Edit `profiles/exit-example.yml' to match your needs.

Once configured run

> ansible-playbook -e profiles/profile-name.yml install-exit.yml

To update the users or gateways list simply run again. Users should not be disrupted
unless a new gateway was added. Even then the disruption should be very minor.

Setting up an Althea node
-------------------------

An Althea intermediary node will pass traffic for other users on the mesh 
as well as provide secure internet acces over the mesh from a configured lan
port. 

Create a file named `hosts` and populate it with the ip addreses
of your exit server like so.

>[intermediary]
>server a
>server b

Profiles are variables files pulled into Ansible for easy customization of what
the playbook will do. Edit `profiles/example.yml' to match your needs.

Once configured run

> ansible-playbook -e profiles/profile-name.yml install-intermediary.yml

To update the Rita version just run again after building a new binary and placing
it in the same folder as the playbook



