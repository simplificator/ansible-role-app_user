# Ansible Role: App User

[![CI](https://github.com/simplificator/ansible-role-app_user/workflows/CI/badge.svg?event=push)](https://github.com/simplificator/ansible-role-app_user/actions?query=workflow%3ACI)

An Ansible role to provision a Linux user without privileges, including distributing authorized keys to it.

## Requirements

N/A

## Role Variables

You need to define the following variable:

* `app_user`: The name of your user which should be created by this role.
* `authorized_keys`: A JSON list of public SSH keys which can login as this user.

## Define authorized_keys and additional_authorized_keys

`authorized_keys` should be defined in group variables. It's a JSON object where the key is `"{{ app_user }}"` and the value is an array of SSH keys. It would look like this:

```yaml
authorized_keys: 
  {
    "{{ app_user }}": [
      "key1",
      "key2",
      "key3"
    ]
  }
```

If you need to add additional keys, e.g. because for one system, a customer of yours has access, you can provide `additional_authorized_keys`. It follows the same format as `authorized_keys`.

```yaml
additional_authorized_keys: 
  {
    "{{ app_user }}": [
      "key1",
      "key2",
      "key3"
    ]
  }
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: myserver
  roles:
    - { role: simplificator.app_user }
  vars:
    authorized_keys: 
      {
        "{{ app_user }}": [
          "key1",
          "key2",
          "key3"
        ]
      }
```

## License

MIT / BSD
