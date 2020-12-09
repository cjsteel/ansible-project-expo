# Controller

## Initial Controller Configuration

* [Initial Controller Configuration](initial-controller-configuration.md)

## Usage

## Activate the Production Virtual Environment

This is done using an aliases which reflect the current (and past) production versions of Ansible and allows new Ansible versions to be added to the system without interfering the OS's base Python (and python applications such as pip) installation or with previous Ansible production version.

- `ansible-2.10.` # Use tab completion with unique command prefix to activate the desired Python virtual environment

## Expo Project Directory layout

```shell
docs/ # mkdocs documentation 
expo/
    ansible.cfg  # active ansible configuration file 
    ansible.cfgs/  # available ansible configurations
        ansible.cfg_testing
        ansible.cfg_production
    base.yml      # base configuration playbook
    controller-base-roles-installation.yml
    controller-bootstrap-roles-installation.sh
    controller-development-roles-installation.yml
    controller-workstation-roles-installation.yml
    docs/         # mkdocs content
        index.md  # mkdocs homepage
inventory/
    testing/      # testing inventory repository
    production/   # production inventory repository
```



