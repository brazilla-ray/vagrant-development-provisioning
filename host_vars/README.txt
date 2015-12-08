All the host-specific variables are set here. The 'dummy_host' file is provided as an example. Each host should have a file in this directory, named for the host. A host named 'foo' would have a vars file here named 'foo'.

The variables that can be set here are:
    ansible_ssh_port:
        This should be the forwarded port that is set up in the Vagrantfile. For example, if you had a machine named 'foo' defined in your Vagrantfile, and the ssh port is forwarded like so -

            foo.vm.network :forwarded_port, guest: 22, host: 2200, auto_correct: false, id: "ssh"

        - the port number to set here would be 2200. Each 'host' port number should be unique, so, 2200, 2201, 2202, etc. Or something similar.
    ansible_ssh_private_key_file:
        Vagrant provides a default key to allow SSH connections to the machine. This is fine for local development, and allows Ansible to connect to the machines. Run 'vagrant ssh-config MACHINE_NAME' while the Vagrant machine ('MACHINE_NAME') is running to see where the key is located.
    hostname:
        The hostname should match the name set in Ansible's host file.
    fqdn:
        Optional. Sets the FQDN of the Vagrant machine.
    domain:
        Optional. Sets the domain name of the Vagrant machine.


