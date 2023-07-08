# system-update

This role can be used to update packages at systems using the dnf package
manager.

The role allows to specify if general updates, bugfixes or security updated
should be applied. To avoid issues with e.g. updated kernel packages, the role
performs a reboot after any package was updated, execpt it is explicitely told
to not do so.

## Requirements

The target system must be able to access update sources.

## Role Variables


## Example Playbooks

The following example show, how to only apply security relevant updates to
target system, supressing the reboot:

~~~yaml
---
- name: Only Security updates w/o reboot
  hosts:
    - foo.example

  gather_facts: false

  roles:
    - role: system_update
      vars:
        var_system_update_packages: false
        var_system_update_bugfix: false
        var_system_update_prevent_reboot: true
~~~

Apply only OS update packages, but no additional security or bugfix updates.
Also, wait 10 seconds before issuing the reboot command:

~~~yaml
---
- name: Apply OS updates
  hosts:
    - foo.example

  gather_facts: false

  roles:
    - role: system_update
      vars:
        var_system_update_security: false
        var_system_update_bugfix: false
        var_system_update_pre_reboot_delay: 10
~~~

## License

MIT

## Author Information

| Date        | Version | Author      |
|-------------|---------|-------------|
| 2023-06-17  | 1.0.0   | Daniel Kuß  |
