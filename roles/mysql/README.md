# MySQL Role

Pulls down the MySQL image from the docker repository and starts a container with that MySQL image.

## Variables

The variables do the following:

```
docker_network_name
```
`docker_network_name` specifies which network to place the docker container into. It's important that all the containers are placed in the same network as they need to communicate with each other.

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

```
db_root_password
```
`db_root_password` specifies the root password.