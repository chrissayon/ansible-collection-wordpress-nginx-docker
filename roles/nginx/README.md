# Nginx Role

Pulls down the Nginx image from the docker repository and starts a container with that Nginx image.

## Role Variables

| Variable                  | Description                                                                                                                                                                   |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `nginx_docker_tag`        | Nginx Docker Tag                                                                                                                                                              |
| `docker_network_name`     | Specifies which network to place the docker container into. It's important that all the containers are placed in the same network as they need to communicate with each other |
| `docker_mysql_hostname`   | Specifies the hostname of the mysql container. This is important as the wordpress container will need to communicate with the mysql database                                  |
| `nginx_server_name`       | Specifies the url you wish to put the nginx.j2 template.                                                                                                                      |
| `docker_base_volume_path` | Specifies the base path of where the volumes will be mounted.                                                                                                                 |
| `ssl`                     | Specify whether you want to use SSL for Nginx. Read below for further information about SSL.                                                                                  |

## SSL

For the SSL variable, this will cause `nginx_https` to be loaded instead of `nginx_http`. This will add one more mapping on the docker volume for `"{{ docker_base_volume_path }}/nginx/ssl:/etc/nginx/ssl/:ro"` so you will need to place it in the `nginx/ssl` folder.

The nginx template (nginx.j2) itself is decided by the user so they have the freedom to name and place it in those folders however they want.

Here is an example of the `SSL` version:

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
