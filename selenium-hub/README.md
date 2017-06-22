selenium-hub
============

This role deploys Selenium Server
and runs it in the _hub_ mode using a system service.

Requirements
------------

The only limitation is to have exactly **one** host in the inventory
group the `selenium-hub` role is applied on.

For example, this inventory part is ok:

    [selenium-hub]
    hub01.example.com

but this will fail:

    [selenium-hub]
    hub01.example.com
    hub02.example.com

as well as section with no hosts:

    [selenium-hub]

Role Variables
--------------

See variables of the [common](../common/README.md) role.
No other variables are defined in this role.

Dependencies
------------

- [common](../common/README.md) role

Example Playbook
----------------

Example inventory:

    [selenium-hub]
    hub.example.com

Running a role with our own values:

    - hosts: selenium-hub
      roles:
        - {
            role: selenium-hub,
            config_dir: /etc/my-selenium,
            selenium_dir: /var/lib/selenium,
            selenium_version: 3.4.0,
            hub_port: 4455
          }

**Note:** As these variables are used in both roles,
`selenium-hub` and `selenium-node`, it is a good practice
to define them in one place, so both roles see
the same values.

For example, a _group_vars/all_ variable file:

    ---
    config_dir: /etc/my-selenium
    selenium_dir: /var/lib/selenium
    selenium_version: 3.4.0
    hub_port: 4455
