# Usage

## Some basic Command examples

### applying the base configuration


```shell
./base.yml -l workstation-003 -e python-interpreter=/usr/bin/python2
```

### Update targeted systems

This is the equivalent of running `apt update && apt-upgrade && apt dist-upgrade` and rebooting after each upgrade.

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


