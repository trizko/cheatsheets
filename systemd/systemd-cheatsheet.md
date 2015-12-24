#### Commands
```bash
# check the status of a unit
$ systemctl status <application>.service

# returns `active` or `inactive` (sets exit code to `0` if active)
$ systemctl is-active <application>.service
# returns `enabled` or `disabled` (sets exit code to `0` if enabled, and `1` if
# disabled)
$ systemctl is-enabled <application>.service
# returns `active` or `failed` (sets exit code to `0` if failed, and `1` for any
# other status)
$ systemctl is-failed <application>.service

# equivalent to -> `systemctl`, list loaded units
$ systemctl list-units

# to list all units
$ systemctl list-units --all
# to filter units by state
$ systemctl list-units --all --state=inactive
# to filter units by state and type
$ systemctl list-units --all --state=inactive --type=service

# to list all unit files in systemd paths, `static` means that the unit file
# does not contain an [INSTALL] section
$ systemctl list-unit-files

# to see the unit file associated with the given unit
$ systemctl cat <application>.service

# to list the dependencies of a unit (recursive search for only target files)
$ systemctl list-dependencies multi-user.target
# to list the dependencies of a unit and all it's dependencies
$ systemctl list-dependencies kubelet.service --all
# to list the reverse dependencies of a unit that must start before or after the
# given unit
$ systemctl list-dependencies kubelet.service --before
$ systemctl list-dependencies kubelet.service --after

# to show the low-level properties of a unit
$ systemctl show docker.service
# to filter by a given property of a unit
$ systemctl show docker.service -p WantedBy

# to mask a unit (cannot be started automatically or manually)
$ systemctl mask flanneld.service
# to unmask
$ systemctl unmask flanneld.service
```

#### Resources
- [Systemd systemctl utility tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units) by Justin Ellingwood
- [Systemd Units and Unit files tutorial](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files) by Justin Ellingwood
