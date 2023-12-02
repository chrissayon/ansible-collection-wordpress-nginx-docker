# Ansible Collection - chrissayon.wordpress_docker

Ansible collection used to deploy a wordpress, mysql, and nginx all within docker containers.

## Installation

Install the collection with:

```
ansible-galaxy collection install chrissayon.wordpress_docker
```

Then, install the dependancies with:

```
ansible-galaxy install -r ~/.ansible/collections/ansible_collections/chrissayon/wordpress_docker/meta/requirements.yml

OR

ansible-galaxy role install geerlingguy.docker
```

## Example Playbook

The following is a playbook example on how to use this collection.

```
- hosts: all
  collections:
  - chrissayon.wordpress_docker

  roles:
  - geerlingguy.docker
  - chrissayon.wordpress_docker.network
  - chrissayon.wordpress_docker.mysql
  - chrissayon.wordpress_docker.wordpress
  - chrissayon.wordpress_docker.nginx
```

The above will completely deploy the application and make it accessable on port 80.
