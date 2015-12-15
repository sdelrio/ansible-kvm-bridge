ansible kvm
===========

Install kvm and bridge interface with ansible on debian.

Requirements
------------

Ansible and acces to a debian 8 machine (probably will work with other versions but not tested).

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

- kvm_groups: libvirt,kvm (groups needed to run kvm on users)
- kvm_users: (user than an use kvm)
  - "{{ ansible_ssh_user }}"
- kvm_cpu: intel or amd, default value is `intel`.
- kvm_phys_interface: interface to bridge, eth0 as default value.
- kvm_bridge_interface: name of the bridge inerface, br0 as default value.
- kvm_bridge_ipv4: configuration for the bridge interfaces, to be added on `/network/intefaces.d/`
```
  - address: 192.168.66.6
  - netmask: 255.255.255.0
  - network: 192.168.66.0
  - broadcast: 192.168.66.255 
#  - gateway: 192.168.66.1
  - bridge_ports: "{{ kvm_phys_interface }}"
  - bridge_stp: 'on'
  - bridge_maxwait: 0
  - address: 192.168.66.6
```


Dependencies
------------

No dependencies. 

Example Playbook
----------------

To install on localmachine having hosts defined localhost as `ansible_connection=local`

```
---
- name: Local computer
  hosts: localhost
  sudo: True
  pre_tasks:
    - name: update APT cache
      apt: update_cache=yes cache_valid_time=28800
      when: ansible_os_family == 'Debian'

  roles:
    - role: kvm
```

License
-------

BSD

