# aspects_sudo

Install `sudo` and manage `/etc/sudoers` configuration.

Currently, no options are available for managing `sudo.conf` configuration.

## Requirements

Set `hash_behaviour=merge` in your ansible.cfg file.

## Role Variables

### `aspects_sudo_enabled`
Boolean. Default `False`. Set `True` if you want to run the tasks in this role.

### `aspects_sudo_sudoers_rules`
* Each sub item represents a single line in `/etc/sudoers`. See sudoers man page for details on what you can set.
* The values in defaults/main.yml are cribbed from Ubuntu 12.04.
* The dictionary is passed through the [Jinja sort filter](http://jinja.pocoo.org/docs/2.10/templates/) (search for "sort"), so you can add order if you are careful. 

### `aspects_sudo_sudoers_privs`
* Each sub item represents a single line in `/etc/sudoers`. See sudoers man page for details on what you can set.
* The values in defaults/main.yml are cribbed from Ubuntu 12.04.
* The dictionary is passed through the [Jinja sort filter](http://jinja.pocoo.org/docs/2.10/templates/) (search for "sort"), so you can add order if you are careful.

## Validation
The `/etc/sudoers` file is run through a validation step before it is saved. If you see errors like:

```yaml
"stdout_lines": ["parse error in /home/vagrant/.ansible/tmp/ansible-tmp-1534201445.64-76120801780564/source near line 7"]}
```
Then you may have sudo syntax errors in your configuration. Try making a temp file with your configuration in it and then use `visudo` to validate it.

## Dependencies
### aspects_packages
[aspects_packages](https://github.com/LaneCommunityCollege/aspects_packages) is used to install `cronie-anacron` on OracleLinux 6. The Vagrant box I used while testing did not have any crontab utility installed. 

If you don't want to use `aspects_packages`, just set `aspects_packages_enabled: False`.

## Example Playbook

```yaml
    - hosts: servers
      roles:
         - aspects_sudo
      vars:
        aspects_sudo_sudoers_rules:
          mailto: 'Defaults mailto="example@example.org"'
```

## License

MIT
