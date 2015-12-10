# vagrant-development-provisioning
Provisioning Vagrant machines via Ansible for local development.

* * *

### Overview

* * *

The goal of this project is to provide a simple way to create local development environments using Ansible to provision a group of Vagrant machines.

It aims to mimic as much as possible the provisioning of a remote server or servers using Ansible. To that end, it does not make use of Vagrant's built-in Ansible provisioner. While that may be simpler and, depending on your needs, preferable, this approach does allow you to take full advantage of Ansible's inventory tools, such as grouping hosts and setting variables for them. 

Using this approach, you could have a Vagrant machine for Rails development, one for Drupal, and so on, all provisioned from a single master playbook, with tasks assigned to each machine as needed.

This project is not meant to create any specific *type* of development environment. The machines will be configured only in the most basic way. It will install nginx for example, but only configure it to serve a simple static page. Each Ansible role is made to be as modular as possible, allowing you to add or remove things as needed.

### Usage

* * *

##### Vagrantfile


The `Vagrantfile` provided here is an example, you should change it to suit your needs. There are three machines defined in this example, you can change that to however many or few you need. Just add or delete config blocks as you see fit. The machine names can be whatever you like. The IP address can be something different, but should be unique for each machine. The host port in the `forwarded port` line can change as well, so long as each is unique.

For more on Vagrant multi-machine setups, consult the [Vagrant docs](https://docs.vagrantup.com/v2/multi-machine/index.html).

##### Inventory

Ansible needs an inventory file; you should create one before anything else. Consult the [Ansible docs](http://docs.ansible.com/ansible/intro_inventory.html) for more on that. It can be named anything you like; 'dev' or something similar is fine.

In that inventory file, you'll be naming all the hosts Ansible will be provisioning. In this case, those will be the various Vagrant machines you define in your `Vagrantfile`. Those hosts should be grouped together in order to take advantage of the `group_vars` file. It will end up looking like this:  
  
        [vagrant]
        vagrant_host
        another_vagrant_host
        and_so_on

The group name is 'vagrant' here, but it can be anything, so long as the vars file in `group_vars` is named the same.

##### Group variables

Speaking of `group_vars`, the file(s) in that directory allow you to define variables for all the members of that group. That way, you only have to define variables common to all your hosts once. 

In this case, there are four defined; `ansible_ssh_host`, `ansible_ssh_user`, `postgres_db_user`, and `mysql_db_user`. The [README](group_vars/README.md) in the `group_vars` directory has more on these variables and their appropriate values.

##### Host variables

In the `host_vars` directory, there should a file for each of your hosts, i.e., your Vagrant machines. The name of the file should match the name of the host, which should probably be the name of the Vagrant machine for clarity's sake.

The variables to set are `ansible_ssh_port`, `ansible_ssh_private_key_file`, `hostname`, `fqdn`, and `domain`. For more on those, consult the [README](host_vars/README.md) in the `host_vars` directory.

##### Roles

The `site.yml` file is the master playbook that will control how the machines are provisioned. It begins with a group of roles that will define a basic state for each machine, including databases and a webserver (NGINX). These roles all reference variables contained in `vars/main.yml`, as well as variables in `host_vars`.

