# App User Ansible role

This role allows to distribute a non-privileged user, e.g. for running Rails applications or as a user for jumphosts.

## Variables

You need to define the following variable:

* `app_user`: The name of your user which should be created by this role.
* `authorized_keys`: A JSON list of RSA keys which can login as this user.
* `additional_authorized_keys`: A JSON list of RSA keys which can login as this user.

## Define authorized_keys and additional_authorized_keys

`authorized_keys` should be defined in group variables. It's a JSON object where the key is `"{{ app_user }}"` and the value is an array of SSH keys. It would look like this:

```yaml
authorized_keys: '{
  "{{ app_user }}": [
    "key1",
    "key2",
    "key3",
}'
```

The quote before the initial curly brace is needed so the `{{ app_user }}` 
variable is correctly rendered out. This allows to overwrite `app_user` on
a host basis.

`additional_authorized_keys` is meant to be defined on a host basis, e.g. 
if you have an external system administrator which should have access to 
your app user on exactly one system. The format of the variable is the same 
as mentioned above for `authorized_keys`.

```yaml
additional_authorized_keys: '{
  "{{ app_user }}": [
    "key1",
    "key2",
    "key3",
}'
```
