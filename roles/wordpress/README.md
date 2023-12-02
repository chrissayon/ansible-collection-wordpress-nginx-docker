# WordPress Role

Pulls down the WordPress image from the docker repository and starts a container with that WordPress image.

## Role Variables

| Variable                    | Description                                                                                                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `wordpress_docker_tag`      | WordPress Docker Tag                                                                                                                                                          |
| `docker_network_name`       | Specifies which network to place the docker container into. It's important that all the containers are placed in the same network as they need to communicate with each other |
| `docker_base_volume_path`   | Specifies the base path of where the volumes will be mounted.                                                                                                                 |
| `docker_wordpress_hostname` | Specifies the hostname of the wordpress container. This will be important as the nginx container will be forwarding requests to this hostname                                 |
| `docker_mysql_hostname`     | Specifies the hostname of the mysql container. This is important as the wordpress container will need to communicate with the mysql database                                  |
| `db_name`                   | Name of the database                                                                                                                                                          |
| `db_user`                   | Username of the database user                                                                                                                                                 |
| `db_password`               | Password of the database user                                                                                                                                                 |
