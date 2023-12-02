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
