# Ansible Role: authselect

This role configures PAM on systems using [authselect](https://github.com/authselect/authselect).

## Requirements

None

## Dependencies

None

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yml
authselect_packages:
  - authselect
  - sssd
```

Controls the packages that will be installed.

```yml
authselect_user_nsswitch_conf:
    passwd: sss files systemd
    shadow: files
    ...
```

Manages the `user-nsswitch.conf` file in authselect. Check
`authselect_user_nsswitch_conf_defaults` variable in `defaults/main.yml` for
the default settings. If you provide changes by setting
`authselect_user_nsswitch.conf`, they will be merged with the default values -
so in the example above only the `passwd` and `shadow` entry will be
overwritten.

```yml
authselect_profile: sssd
```

Set the authselect profile that should be used. Note that this role does not
create custom profiles.

```yml
authselect_features: []
```

A list of features that should be enabled for the specified profile.

```yml
authselect_force: false
```

Applies the `--force` flag to the `authselect select` command. Note that this
will implicitly set to true when the role detects that no profile is
configured yet (otherwise `authselect` would throw errors)

## Example Playbook

```yml
- hosts: servers
  roles:
    - smlloyd.authselect
```

## License

Beer License.
