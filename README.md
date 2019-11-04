Role Name
=========

This role install & configure Hitachi RAID Manager (CCI) on CentOS7

Install from Ansible Galaxy
------------------------------------

`ansible-galaxy install miquelmariano.hitachicci`

Changelog
------------

29.07.2018 | Add new version of hitachi CCI

04.11.2019 | Add new version of hitachi CCI (01-53-03)


Requirements
------------

No requirements

Role Variables
--------------

No defined variables but is necessary edit your horcmXXX.conf placed on templates dir.

Example:

```
		HORCM_MON
		#Instacia que controla G800 GS
		#ip_address        service         poll(10ms)     timeout(10ms)
		127.0.0.1          60300          1000              3000

		HORCM_CMD
		\\.\IPCMD-172.25.32.12-31001    \\.\IPCMD-172.25.34.13-31001

		HORCM_LDEV
		GS_GAD  0000-0000       000000  00:00   0
		GS_GAD  0001-0001       000000  00:01   0
		GS_GAD  0002-0002       000000  00:02   0
		GS_GAD  0003-0003       000000  00:03   0
		IX_GAD  0004-0004       000000  00:04   0

		HORCM_INST
		#dev_group        ip_address      service
		IX_GAD  127.0.0.1       60301
		GS_GAD  127.0.0.1       60301

```

Dependencies
------------

No dependencies

Example Playbook
----------------

```yaml
##hitachiCCI.yml

- hosts: ansible
  user: root
  tasks:
     - name: Ensure that role are up to date
       command: ansible-galaxy install --force {{ item }}
       with_items:
          - miquelmariano.hitachicci
       when:
          - update_mode | default(False)
       tags: update
       ignore_errors: yes

- hosts: "{{ servers }}"
  user: root
  roles:
    - role: miquelmariano.hitachicci
```

Usage
-------

`ansible-playbook playbooks/hitachiCCI.yml -i inventory/servers -e "servers=server1 install=true update_mode=true" --tags=install`


License
-------

BSD

Author Information
------------------

[miquelMariano.github.io](https://miquelmariano.github.io)  | [@miquelMariano](https://twitter.com/miquelMariano)
