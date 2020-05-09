# Guide

Configuration and usage guide for orchestrating a systems parc of (Ansible) controllers, servers and workstations using Ansible

## Park Members

Parc membership requirements and services

### BIOS / (U)EFI and Hardware

Requirements and setting

#### Wake-on-LAN (**WoL**)

#### Network booting

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

