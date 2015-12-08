#### Group variables

When you create an inventory file for use with Ansible, place the Vagrant hosts in a group, like so:

    [vagrant]
    vagrant_host
    another_vagrant_host
    and_so_on

That way, you can set some common variables here, without having to repeat them for each host. The variables you can set here are:  

`ansible_ssh_host`
This should be 127.0.0.1, but maybe there's some case where another address would be better.  
    
`ansible_ssh_user`
Probably this should be 'vagrant', as that is Vagrant's default, but it could be something else if you have Vagrant set up that way.  

`postgres_db_user`
If you want to set up Postgresql with the same user for all the machines in the [vagrant] group, set it here. For example, it could be set to 'vagrant' here, and all the machines would have the default Vagrant user as a database user. Otherwise, remove or comment this out, and set it elsewhere.  

`mysql_db_user`
Same as above.
