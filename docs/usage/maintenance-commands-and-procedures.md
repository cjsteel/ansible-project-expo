# Maintenance commands and procedures

#### IMPORTANT

You will almost always want to use the `-l` flag in order to limit the targets of your Ansible commands.are certain of whet the outcome will be in a production environment you might apply to additional groups of systems. 

The `-l` or `--limit` flag is used on all Ansible commands in order to limit the command to a particular system or group of systems.

## Basic Command Examples



### Applying a base configuration

Applied to all system to be added to a network

* Ensures that new systems have all configuration requirements for membership on the network
* Applies required configuration for basic security and administration, for example:
  * Upgrades OS and all applications
  * Creation of administrative user and initial permissions
  * Firewall
  * Fail2ban
  * Any other requirements that **all systems** must meet before connecting to the target network
  * Similar to the Ansible concept of a `common.yml` playbook.

#### Command example

```shell
./base.yml -l workstation-003 -e python-interpreter=/usr/bin/python2
```

### Update all targeted systems

This is the equivalent of running `apt update && apt-upgrade && apt dist-upgrade` and rebooting after ea>

```shell
`./update -l workstations -e reboot=yes
```

### Shutdown targeted systems

Does exactly what you would expect

```shell
./shutdown -l workstations
```

### Power on all targeted WOL enabled workstations


```shell
./wakeonlan -l room-001
```
