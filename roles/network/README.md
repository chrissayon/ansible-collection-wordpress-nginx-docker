# Docker Network Role

Create a docker network.

## Role Variables

| Variable              | Description                                                                                                                                                                   |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `docker_network_name` | Specifies which network to place the docker container into. It's important that all the containers are placed in the same network as they need to communicate with each other |
