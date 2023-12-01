# WordPress Role

Pulls down the WordPress image from the docker repository and starts a container with that WordPress image.

## Variables
```
docker_network_name
```
`docker_network_name` specifies which network to place the docker container into. It's important that all the containers are placed in the same network as they need to communicate with each other.

```
docker_base_volume_path: /home/wordpress_docker
```
`docker_base_volume_path` specifies the base path of where the volumes will be mounted. 

```
docker_wordpress_hostname: wordpress_host
```
`docker_wordpress_hostname` specifies the hostname of the wordpress container. This will be important as the nginx container will be forwarding requests to this hostname

```
docker_mysql_hostname
```
`docker_mysql_hostname` specifies the hostname of the mysql container. This is important as the wordpress container will need to communicate with the mysql database.

```
db_name
```
`db_name` specifies the name of the database.

```
db_user
```
`db_user` specifies the username.

```
db_password
```
`db_password` specifies the password.
