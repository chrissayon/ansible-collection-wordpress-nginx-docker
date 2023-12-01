# Nginx Role

Pulls down the Nginx image from the docker repository and starts a container with that Nginx image.

## Variables

```
docker_mysql_hostname
```
`docker_mysql_hostname` specifies the hostname of the mysql container. This is important as the wordpress container will need to communicate with the mysql database.

```
nginx_server_name
```
`nginx_server_name` specifies the url you wish to put the nginx.j2 template.

```
docker_nginx_hostname
```
`docker_nginx_hostname` specifies the hostname of the nginx container.

```
docker_base_volume_path: /home/wordpress_docker
```
`docker_base_volume_path` specifies the base path of where the volumes will be mounted. 

```
docker_network_name
```
`docker_network_name` specifies which network to place the docker container into. It's important that all the containers are placed in the same network as they need to communicate with each other.

