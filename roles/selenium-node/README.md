selenium-node
=============

This role deploys one or more nodes on a host.
One node consists of several system services and
each node runs on a separate display.

Deployed services per node:
- `xvfb`: virtual framebuffer X server
- `openbox`: window manager
- `vnc`: x11vnc server
- `selenium-node`: Selenium Server running in _node_ mode

All nodes are then managed by `selenium-nodes` service.

Role Variables
--------------

Along with variables from the [common](../common/README.md) role,
this role also uses variables with following defaults:

    hub_host: "{{ groups['selenium-hub'][0] }}"
    nodes: 4
    browser_capabilities:
      -
        browser_name: firefox
        browser_version: ""
    firefox_package: firefox
    chrome_package: chromium
    geckodriver_ver: 0.17.0
    chromedriver_ver: 2.30

`hub_host` variable is by default set to the first host
from the `selenium-hub` group. If your inventory group
with Selenium Hub host has a different name, you need to set
it to that host.
For convenience, it is recommended to use
group named `selenium-hub` for your Hub machine.

Dependencies
------------

- [common](../common/README.md) role

Example Playbook
----------------

Specifying nodes in the inventory:

    [selenium-nodes]
    node1.example.com nodes=4
    node2.example.com nodes=8

Running a role with our own values:

    - hosts: selenium-nodes
      roles:
        - { role: selenium-node, nodes: 8, geckodriver_ver: 0.17.0 }

Putting all variables in a variable file, e.g.,
_group_vars/selenium-nodes_:

    ---
    hub_host: "{{ groups['my-hub'][0] }}"
    nodes: 6
    browser_capabilities:
      -
        browser_name: firefox
        browser_version: "52"
      -
        browser_name: chrome
        browser_version: ""
    firefox_package: firefox-52*
    chrome_package: chromium
    geckodriver_ver: 0.17.0
    chromedriver_ver: 2.30
