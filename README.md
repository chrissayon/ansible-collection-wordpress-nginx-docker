# Ansible Collection - chrissayon.wordpress_docker

Ansible collection used to deploy a wordpress, mysql, and nginx all within docker containers.

The Nginx container has both port 80 and 443 open so the moment it is run, so it will start serving traffic once its running.

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

## Pre-requisites

You will need to create a file at `templates/nginx.j2` structured like the following:

```
server {
    listen 80;
    listen [::]:80;
    server_name {{ nginx_server_name }};

    root   /var/www/html;
    index  index.php;

    location / {
        proxy_pass http://{{ docker_wordpress_hostname }}:80;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

The `nginx_server_name` is a role variable in the `nginx` role that is used for specifying the `server_name`.

The `docker_wordpress_hostname` is the hostname of the `wordpress` docker container. Because both the `wordpress` and `nginx` container are both inside the docker network, these will have their own hostname.

### Optional SSL

You can create an `SSL` version of this which would be like the following:

```
server {
    listen 80;
    listen [::]:80;
    server_name {{ nginx_server_name }};

    location / {
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl;
    server_name {{ nginx_server_name }};

    root   /var/www/html;
    index  index.php;

    ssl_certificate /etc/nginx/ssl/fullchain.pem;
    ssl_certificate_key /etc/nginx/ssl/privatekey.pem;
    ssl_trusted_certificate /etc/nginx/ssl/intermediatecertificate.pem;

    location / {
        proxy_pass http://{{ docker_wordpress_hostname }}:80;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

You will need to handle the mapping and handling of the certificates yourself.

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
