# Ansible Ubuntu MySQL

[![Travis CI](https://img.shields.io/travis/fabschurt/ansible-role-ubuntu-mysql/master.svg)](https://travis-ci.org/fabschurt/ansible-role-ubuntu-mysql)

This role will basically install MySQL 5.7 and create some databases and users.
For now, privilege handling is very basic: you can only declare full database
access for specific users.

## Requirements

* Ubuntu 18.04 remote host(s) with root access
* Ansible >= 2.4

## Role variables

This role is configurable with the following variables:

* `mysql_databases`: a list of databases that should exist
* `mysql_users`: a list of users that should exist; each element in this list is
  an object with the following mandatory properties:
    - `username`: the user’s name
    - `password`: the user’s password (in native hashed form, please see [here](https://dev.mysql.com/doc/refman/5.7/en/password-hashing.html))
    - `owned_databases`: a list of databases over which the user will have full
      privileges (except `GRANT`)

See the [Example playbook](#example-playbook) section below for an example of
how to set these variables.

## Example playbook

This is an example playbook that demonstrates how you would use the role,
provided that you’ve [installed](https://galaxy.ansible.com/docs/using/installing.html)
it already:

```yaml
- hosts: …
  roles:
    - role: fabschurt.ubuntu_mysql
      mysql_databases:
        - db1
        - db2
      mysql_users:
        -
          username: john
          password: '*06C0BF5B64ECE2F648B5F048A71903906BA08E5C' # test1
          owned_databases:
            - db2
        -
          username: jack
          password: '*7CEB3FDE5F7A9C4CE5FBE610D7D8EDA62EBE5F4E' # test2
          owned_databases:
            - db1
            - db2

```

## License

This software package is licensed under the [MIT License](https://opensource.org/licenses/MIT).
