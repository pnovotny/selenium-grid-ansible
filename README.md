About
=====
Ansible-based automation for Selenium Grid deployment.

This repository provides two roles:
- [selenium-hub](selenium-hub/README.md):
deployment of a Selenium Hub
- [selenium-node](selenium-node/README.md):
deployment of Selenium Node(s)

Installation
------------

Create requirements file _requirements.yml_:

    ---
    - src: https://github.com/pnovotny/selenium-grid-ansible.git
      version: master

Install roles:
`ansible-galaxy install -r requirements.yml --roles-path <path>`

Usage
-----

The following example shows deployment of a:
- Selenium Hub instance on host _hub.example.com_
- 4 Selenium Node instances on host _hub.example.com_
- 8 Selenium Node instances on hosts _node1.example.com_
and _node2.example.com_

Inventory:

    [selenium-hub]
    hub.example.com

    [selenium-nodes]
    hub.example.com nodes=4
    node1.example.com
    node2.example.com

Playbook:

    ---
    - hosts: selenium-hub
      roles:
        - { role: selenium-grid-ansible/selenium-hub }

    - hosts: selenium-nodes
      roles:
        - { role: selenium-grid-ansible/selenium-node }

Variable file _group_vars/all_:

    ---
    # common variables for Hub and Node(s):
    config_dir: /etc/selenium-grid
    selenium_dir: /opt/selenium-grid
    selenium_version: 2.53.1
    hub_port: 4444

    # Node variables:
    # (these can be set specifically for a particular group or host)
    nodes: 8
    browser_capabilities:
      -
        browser_name: firefox
        browser_version: ""
      -
        browser_name: chrome
        browser_version: ""
    firefox_package: firefox
    chrome_package: chromium
    geckodriver_ver: 0.17.0
    chromedriver_ver: 2.30
