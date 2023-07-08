# ansible-role-



## Requirements



## Role Variables

The following table shows all variables used by the role which can be set to
influence the role behaviour.

| Variable                            | Type  | Default | Comment                                                                                                                         |
|-------------------------------------|-------|---------|---------------------------------------------------------------------------------------------------------------------------------|
| var_system_update_gather_timeout    | int   | 10      | Specify the timeout for the gather fact command.                                                                                |
| var_system_update_packages          | bool  | true    | Specify whether system packages should be updated.                                                                              |
| var_system_update_security          | bool  | true    | Specify whether additional security updates should be applied.                                                                  |
| var_system_update_bugfix            | bool  | true    | Specify whether additional bugfix updates should be applied.                                                                    |
| var_system_update_update_cache      | bool  | true    | Specify whether the package manager cache should be updated prior to searching/applying updates.                                |
| var_system_update_prevent_reboot    | bool  | false   | Specify whether the reboot after packages changed during the update should be prevented.                                        |
| var_system_update_pre_reboot_delay  | int   | 0       | Specify the amount of seconds to wait before issuing the reboot command.                                                        |
| var_system_update_reboot_delay      | int   | 600     | Specify the amount of seconds to wait after the reboot command was issued before considering the target server as unresponsive. |

## Role Tags

This role has no tags.

## Role Vaults

This role uses no Ansible vaults.

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
