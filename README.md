# Leaf Spine Deployment with Ansible
A series of playbooks which will create and update a leaf-spine fabric comprised of **Cisco NX-OS** devices.

This is project is built on premise of a 10-switch leaf-spine fabric, including the following:

* 4 x Spine Switches
* 4 x Leaf Switches (two vPC pairs)
* 2 x Border Leaf Switches

Four VLANs are created on each switch, based around a basic VMware NSX deployment:

* VTEP
* vSphere Management
* Storage Replication
* vMotion

_These playbooks easily be adapted to meet a number of different use-cases and requirements._

## Getting Started

### Prerequisites

This playbook uses the resource modules introduced in Ansible 2.9; therefore, ensure you have Ansible 2.9 installed. CDP must be enabled on the devices to allow for interface descriptions to be dynamically created.

```
$ ansible --version
ansible 2.9.0
  config file = None
  configured module search path = ['~/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/Cellar/ansible/2.9.0/libexec/lib/python3.7/site-packages/ansible
  executable location = /usr/local/bin/ansible
  python version = 3.7.5 (default, Nov  1 2019, 02:16:32) [Clang 11.0.0 (clang-1100.0.33.8)]
```

Target devices must be *bootstrapped* with a management IP address, and must be reachable by the Ansible control node (i.e.: wherever you're running the `ansible-playbook` command from).

### Installing

Clone this repository to your Ansible control node or workstation:

```
git clone https://github.com/MrThePlague/ansible-leaf-spine.git
```

## Defining the Inventory

Edit the inventory.ini to list your devices, and group them as you please, but esure that the ansible_network_os variable is defined correctly for each group of devices.

## Running the Playbook(s)

The entire fabric can be deployed and/or updated by calling the main `deploy-fabric.yml` playbook.

```
$ ansible-playbook -i <inventory>.ini -u <username> -k deploy-fabric.yml
```

Individual functions (spine/leaf/border) can be deployed by using the function-specific playbook, e.g.:

```
$ ansible-playbook -i <inventory>.ini -u <username> -k deploy-spine.yml
```

And specific subsections of the configuration can be called by utilising the playbook tags, for example the below will deploy only NTP-related configuration to all devices within the fabric.:

```
$ ansible-playbook -i <inventory>.ini -u <username> -k deploy-fabric.yml -t ntp
```

## Feature Requests and To-Do

Feature requests and backlog items will be managed through the GitHub Issues

## Issues

If you discover an issue, of which undoubtedly there are many, please submit a **GitHub issue**.

## Making Changes

To make changes and/or contribute to this repository, please **fork** the repository, and make a **pull request**.