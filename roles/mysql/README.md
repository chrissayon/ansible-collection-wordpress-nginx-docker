# MySQL Role

Pulls down the MySQL image from the docker repository and starts a container with that MySQL image.

## Role Variables

| Variable                | Description                                                                                                                                                                   |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `mysql_docker_tag`      | MySQL Docker Tag                                                                                                                                                              |
| `docker_network_name`   | Specifies which network to place the docker container into. It's important that all the containers are placed in the same network as they need to communicate with each other |
| `docker_mysql_hostname` | Specifies the hostname of the mysql container. This is important as the wordpress container will need to communicate with the mysql database                                  |
| `db_name`               | Name of the database                                                                                                                                                          |
| `db_user`               | Username of the database user                                                                                                                                                 |
| `db_password`           | Password of the database user                                                                                                                                                 |
| `db_root_password`      | Root password of the database                                                                                                                                                 |
