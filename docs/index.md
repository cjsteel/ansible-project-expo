# Ansible Expo

## Commands

* `./base.yml -l workstation-003 -e python-interpreter=/usr/bin/python2 - Apply the base configuration to a workstation
* `./update -l workstations -e reboot=yes - Update all workstation and reboot them
* `./shutdown -l workstations` -Shutdown all workstaions
* `./wakeonlan -l workstations` - Power on all workstations

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Setting up a development platform

* [Development](development/index.md)


