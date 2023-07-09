# system-update

![Ansible Lint](https://github.com/cthullu/ansible-role-system-update/actions/workflows/ansible-lint.yml/badge.svg)

This role can be used to update packages at systems using the dnf or apt package
manager.

The role allows to specify if general updates, bugfixes or security updated
should be applied. To avoid issues with e.g. updated kernel packages, the role
performs a reboot after any package was updated, execpt it is explicitely told
to not do so.

## Requirements

The target system must be able to access update sources.

## Role Variables

The following variables are used by the role and set inside the
`defaults/main.yml`:

~~~yaml
var_system_update_gather_timeout: 10
var_system_update_packages: true
var_system_update_security: true
var_system_update_bugfix: true
var_system_update_update_cache: true
var_system_update_prevent_reboot: false
var_system_update_pre_reboot_delay: 5
var_system_update_reboot_delay: 600
~~~

| Variable                            | Type    | Default | Comment                                                                                                               |
|-------------------------------------|---------|---------|-----------------------------------------------------------------------------------------------------------------------|
| var_system_update_bugfix            | boolean | true    | Specify if bugfix updates should be applied.                                                                          |
| var_system_update_gather_timeout    | int     | 10      | Specify the timeout value for gathering system facts.                                                                 |
| var_system_update_packages          | boolean | true    | Specify if updates for all packages should be applied.                                                                |
| var_system_update_pre_reboot_delay  | int     | 5       | Specify the timeout (in seconds) to wait between announcing the reboot and performing it.                             |
| var_system_update_prevent_reboot    | boolean | false   | Specify if the reboot after applying updates should be prevented.                                                     |
| var_system_update_reboot_delay      | int     | 600     | Specify the time (in seconds) to wait after issuing the reboot command before considering the target as unreachable.  |
| var_system_update_security          | boolean | true    | Specify if security updates should be applied.                                                                        |
| var_system_update_update_cache      | boolean | true    | Specify if a package cache update should be forced prior to searching for updates.                                    |

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
| 2023-07-09  | 1.0.0   | Daniel Kuß  |
