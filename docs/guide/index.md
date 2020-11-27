# Guide

Configuration and usage guide for orchestrating a systems parc of (Ansible) controllers, servers and workstations using Ansible

## System Requirements

* BIOS / (U)EFI Settings
  * Wake-on-LAN (**WoL**)
  * Network booting

* DNS or ability to edit controllers `/etc/hosts` file

# Orchestrating Systems

## Base configuration

All systems on our imaginary LAN must have a (minimal) base configuration before the may become LAN members.

In this example we will apply the (minimal) base configuration to a new system called **workstation-003**

### Requirements

- resolvable host name
- must be included in the controllers inventory
- must have an administrative user
- must be reachable via ssh
- known_hosts

## Resolvable Host Name

### DNS

```
nslookup workstation-003
```

### /etc/hosts file

When developing it may sometimes be preferable to add a new host to the controllers `/etc/hosts`. In this example our controller is applying the base configuration to three new system on a (protected) private network:

```
127.0.0.1   localhost
127.0.1.1   controller-001
192.168.1.124   workstation-001
192.168.1.125   workstation-002
192.168.1.126   workstation-003

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

Once the hostname and ip address have been added to the controllers `/etc/hosts` file it should be reachable by the hostname *even though the hostname on the target system, workstation-003 may not be correct at the moment*.

## Important!

If you logged into your new host as the administrative user in order  to get the ip address, make sure you logout once you are finished,  otherwise, you application of the base configuration will fail as the  user will still have running processes! 

## Connectivity test

We manually connect to the new host via ssh for our controller in order to ensure that everything is working as it should.

This will also allow us to add our controller to the known_hosts file on the new system, or in some development situations, will give us an  opportunity to remove any stale known_hosts entries.

In this example our remote administrative user is the user *julie*

```
ssh julie@workstation-003
```

If this example I am connecting from a controller running Ubuntu  20.04 and I get the following message as it is the first time I am  connecting to a host named **workstation-003**.

```
The authenticity of host 'workstation-003 (192.168.1.100)' can't be established.
ECDSA key fingerprint is SHA256:vXCJtTry4lMOc3cwMQ50vdFRG9JyR9jovZWs4XYY+JY.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

As this is a private network running DHCP, I have connected to other  hosts using the IP 192.168.0.100 previously and my output looks like  this:

```
Warning: Permanently added 'workstation-003' (ECDSA) to the list of known hosts.
Warning: the ECDSA host key for 'workstation-003' differs from the key for the IP address '192.168.1.100'
Offending key for IP in /home/csteel/.ssh/known_hosts:5
Are you sure you want to continue connecting (yes/no)? no
```

I remove the 5th line from my controllers (development system) `~/.ssh/known_hosts` file and try and connect again:

```
ssh julie@workstation-003
```

This time I am prompted for the admin users password:

```
Warning: Permanently added the ECDSA host key for IP address '192.168.1.100' to the list of known hosts.
julie@workstation-003's password: 
```

Once I type in the correct password, "mypassword", with no quoted in this example, I am able to connect:

```
julie@workstation-003's password: 
Welcome to Ubuntu 20.04 LTS (GNU/Linux 5.4.0-29-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

Last login: Wed May  6 19:17:44 2020 from 192.168.1.101
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

julie@ubuntu:~$ 
```

SSH is working correctly so I exit and move on to the next step

```
julie@ubuntu:~$ exit
```

### ssh agent

The OpenSSH authentication agent will be used to hold private keys used for public key authentication.

When the ssh-agent is started, it prints the shell commands required to set its environment variables.

SSH looks at these environment variables and uses them to establish a connection to the agent.

These environment variables are evaluated in the calling shell, bash or csh for example.

Here we evaluate the environment variables from the terminal  (probably the bash shell in many cases) and if ssh-agent is installed  and running we should get ssh-agents PID (Process ID) as output.

Evaluation command:

```
eval `/usr/bin/ssh-agent -s`
```

Output example:

```
Agent pid 376452
```

### ssh-add

ssh-agent initially does not have any private keys.

ssh-add is used to add one or more private key identities to the OpenSSH authentication agent (ssh-agent). 

Private keys can be added using **ssh-add** or by ssh when AddKeysToAgent is set in ssh_config.

Multiple keys (identities) may be stored in ssh-agent concurrently and ssh will automatically use them if present.

In addition to adding keys, ssh-add can also be used to remove keys  from ssh-agent and to query the keys that are currently held by the  agent.

In the previous section we confirmed that the ssh-agent was installed and running. Now we will add a private key to the ssh-agent

If all is as it should be, running the following command should  prompt you for the keys pass phrase and will remember it on your local  system (the controller) and it will be automatically provided when ssh  requests it:

```
/usr/bin/ssh-add
Enter passphrase for /home/csteel/.ssh/id_rsa: my top secret pass phrase is this
```

If you provided the correct pass phrase you will get the following output and you are ready to move on to the next step:

```
Identity added: /home/csteel/.ssh/id_rsa (/home/csteel/.ssh/id_rsa)
```

### inventory/production/hosts

In this example we see that **workstation-003** has been added to the **[workstations]** section of our *ini* style hosts file:

```
[controllers]
controller-001
controller-002

[servers]
server-001
server-002

[workstations]
workstation-001
workstation-002
workstation-003

[base:children]         
controllers
servers
workstations
```

In the **[base:children]** section we see that **controllers**, **servers** and **workstations** are all *children* of the **base** configuration section. In other words systems in the **controllers**, **servers** and **workstations** sections can all have the base configuration applied to them.

## `ansible.cfg` file

I want to make sure that `ansible.cfg` is pointing to the correct inventory file so I cat it:

```
cat ansible.cfg | grep inventory
```

Output example:

```
log_path = inventory/testing/log/ansible.log
inventory = inventory/testing
```

ansible.cfg is pointing to the testing inventory so I can manually edit it or run the included `./config.sh` script like this:

```
./config.sh production
```

and confirm in the output that we are now using the production inventory:

```
production
Copying production to ansible.cfg
log_path = inventory/production/log/ansible.log
inventory = inventory/production
```

## Applying the base configuration

### inventory/production/group_vars/all

Before applying the base configuration you will want to take a look at the projects group_vars:

```
nano inventory/production/group_vars/all
```

`group_vars/all` contains variables that will be used for  all systems. Since the base configuration will be applied to all systems this is the perfect place to set variables for things that all systems  have in common. For this project, that includes local users on each  system for (manual) administration as well as a user for executing  automated activities.

### IMPORTANT

You will probably want to change the **state** for the temporary user *julie* to be **present** before applying the base configuration. You want to do this because:

- You will be executing the base configuration as *julie* 

### ansible command run

```
./base-system-configuration.yml -l "workstation-003" -kK -e ansible_user=julie -e ansible_python_int
```



## Controller(s)

### Controller setup

##### Requirements

###### Repositories

* Project repository
  * clone or copy ansible-project-expo
* Production inventory repository
  * a private repository is recommended
  * ansible-inventory-production
* ssh key pair
  * pass phrase made of seven or more random words recommended

## Controllers, Servers and Workstations

All parc member systems must have the current base configuration applied in order to be  members of the LAN or WAN.

### Security

At this time the base configuration includes a basic firewall, fail2ban and applies a more restricted umask for all local users.

The best security is continuous integrated rather than applying security "on top" of static configurations. 

