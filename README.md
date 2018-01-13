# aspects_sudo

Install ```sudo``` and manage ```/etc/sudoers``` configuration.

Currently, no options are available for managing ```sudo.conf``` configuration.

## Requirements

Set ```hash_behaviour=merge``` in your ansible.cfg file.

## Role Variables

All default variable values can be overridden in other vars files.

**Warning**: Because rules and privs are dictionaries, the order each line appears in ```/etc/sudoers``` cannot be guaranteed.

* ```aspects_sudo_package_name```
    * Set the package name for various OS families.
* ```aspects_sudo_sudoers_rules``` and ```aspects_sudo_sudoers_privs```
    * Each sub item represents a single line in ```/etc/sudoers```. See sudoers man page for details on what you can set.
    * The values in defaults/main.yml are cribbed from Ubuntu 12.04.
    * Both are passed through the [Jinja sort filter](http://jinja.pocoo.org/docs/2.10/templates/) (search for "sort"), so you can add some order if you are careful.

## Example Playbook

```yaml
    - hosts: servers
      roles:
         - aspects_sudo
      vars:
        aspects_sudoers_rules:
          mailto: 'Defaults mailto="example@example.org"'
```

## License

MIT
