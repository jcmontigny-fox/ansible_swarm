Ansible Swarm Role
==================

A very simple role to quickly set up a Swarm mode cluster using docker-ce.

Requirements
------------

This role should be applied to all hosts (managers and workers) taking part in the cluster.

Role Variables
--------------

__Defaults__
Required variables
- `swarm_managers_ansible_group` : the ansible group containing the managers ; no default value
- `swarm_workers_ansible_group` : the ansible group containing the workers ; no default value

Optional variables
- `swarm_docker_group_members` : list of unix users that need to access the docker CLI ; undefined by default
- `swarm_network_interface` : network interface to use ; defaults to ansible default ipv4 interface
- `swarm_network_address` : ipv4 address to use ; defaults to the ipv4 address of `swarm_network_interface`
- `swarm_network_port` : port to use for cluster management ; defaults to 2377

Other optional variables : release channel for docker
- Debian
  - `swarm_apt_release_channel` : defaults to "stable"


__Vars__
Repository keys for docker (url and fingerprint/id)
- Debian
  - `swarm_apt_repo_key_url_debian` : url to fetch the gpg key
  - `swarm_apt_repo_key_id_debian` : key fingerprint
  - `swarm_apt_repository` : repository to add

Dependencies
------------

None

Example Playbook
----------------

Minimal call :

    - hosts: servers
      become: true
      roles:
        - jcmontigny.ansible_swarm
      vars:
        - swarm_managers_ansible_group: swarm_managers
        - swarm_workers_ansible_group: swarm_workers

Call to add privileges to some users to the docker CLI (example on AWS)

    - hosts: servers
      become: true
      roles:
        - jcmontigny.ansible_swarm
      vars:
        - swarm_managers_ansible_group: swarm_managers
        - swarm_workers_ansible_group: swarm_workers
        - swarm_docker_group_members:
          - admin

License
-------

MIT

Author Information
------------------

Jean-Christophe Montigny ( https://github.com/jcmontigny )  
With inspiration from the role by atosatto ( https://github.com/atosatto/ansible-dockerswarm ) with some modifications