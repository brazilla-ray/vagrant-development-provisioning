# vagrant-development-provisioning
Provisioning Vagrant machines via Ansible for local development.

* * *

### Usage

* * *

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
