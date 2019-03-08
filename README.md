# uwsgi

[![Build Status](https://img.shields.io/travis/infOpen/ansible-role-uwsgi/master.svg?label=travis_master)](https://travis-ci.org/parkoview/ansible-role-uwsgi.svg?branch=master)
[![Build Status](https://img.shields.io/travis/infOpen/ansible-role-uwsgi/develop.svg?label=travis_develop)](https://travis-ci.org/parkoview/ansible-role-uwsgi.svg?branch=develop)
[![Ansible Role](https://img.shields.io/ansible/role/12481.svg)](https://galaxy.ansible.com/parkoview/uwsgi/)

Install uwsgi package.

Forked and mutilated from infOpen/ansible-role-uwsgi. While cleverly written the original role prevents passing multiple environment variables to apps because of the dummy yaml parser that uwsgi uses. libyaml could be another way to circumvent the issue. Anyway, this fork uses a list instead of a dict to generate an ini configuration file.

## Requirements

This role requires Ansible 2.2 or higher,
and platform requirements are listed in the metadata file.

## Testing

This role use [Molecule](https://github.com/metacloud/molecule/) to run tests.

Local and Travis tests run tests on Docker by default.
See molecule documentation to use other backend.

Currently, tests are done on:
- Debian Jessie
- Ubuntu Trusty
- Ubuntu Xenial

and use:
- Ansible 2.2.x
- Ansible 2.3.x
- Ansible 2.4.x

### Running tests

#### Using Docker driver

```
$ tox
```

## Role Variables

### Default role variables

``` yaml
# Installation vars
uwsgi_install_mode: 'package'
uwsgi_packages: "{{ _uwsgi_packages }}"
uwsgi_service_name: 'uwsgi'

# Configuration vars
uwsgi_configuration_available_path: "{{ _uwsgi_configuration_available_path }}"
uwsgi_configuration_enabled_path: "{{ _uwsgi_configuration_enabled_path }}"
uwsgi_configuration_owner: 'root'
uwsgi_configuration_group: 'root'
uwsgi_configuration_mode: '0640'
uwsgi_apps: []

# Handler management
uwsgi_restart_handler_enabled: True
```

### Debian family variables

``` yaml
# Package management
_uwsgi_packages:
  - name: 'uwsgi'
  - name: 'uwsgi-plugin-python'
  - name: 'uwsgi-plugin-python3'

# Configuration management
_uwsgi_configuration_available_path: '/etc/uwsgi/apps-available'
_uwsgi_configuration_enabled_path: '/etc/uwsgi/apps-enabled'
```

## Dependencies

None

## Example Playbook

``` yaml
- hosts: servers
  roles:
    - { role: parkoview.uwsgi }
```

## License

MIT

## Author Information

Alexandre Chaussier (for Infopen company)
- http://www.infopen.pro
- a.chaussier [at] infopen.pro
