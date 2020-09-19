Secure SSH
==========

This document describes some simple steps that improve the security of your SSH
installation. That steps are include:

* Disable the empty password login. Empty password is a **very bad** idea.

* Disable remote root login. The preferred way to gain root permissions is use
  `su` or `sudo` command.

* Disable password login (make sure you have a key installed!).

* Enable [PAM](http://en.wikipedia.org/wiki/Pluggable_authentication_modules).

Role Variables
--------------

The desired behavior can be refined via variables.

Option | Description
--- | ---
`sshd` | Name of ssh daemon, default is `ssh`.
`sshd_config` | Path to ssh daemon config, default is `/etc/ssh/sshd_config`.

For example, you can override default variables by passing it as a parameter to
the role like so:

```yaml
roles:
    - { role: ., sshd: sshd }
```

Or send them via command line:

```bash
ansible-playbook test.yml --extra-vars "sshd_config=/etc/sshd_config"
```

Example Playbook
----------------

The example below uses `sudo` to play book on your localhost via local
connection.

```bash
ansible-playbook test.yml \
    -i hosts.example \
    -c local \
    -s --ask-sudo-pass
 ```

```yaml
# file: test.yml
- hosts: local
  roles:
    - { role: ., sshd: ssh, sshd_config: /etc/sshd_config }
```

License
-------

Licensed under the [MIT license](http://mit-license.org/vitalk).

Author Information
------------------

Created by Vital Kudzelka.

Don't hesitate create [a GitHub Issue](https://github.com/vitalk/ansible-secure-ssh/issues) if you have any bugs or suggestions.
