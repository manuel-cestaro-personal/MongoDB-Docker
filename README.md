# MongoDB with Docker
Example of MongoDB with Docker container.
References:
- https://hub.docker.com/_/mongo
- https://www.mongodb.com/compatibility/docker

## Objective
The goal is to create a MongoDB container that saves data persistently and easily copied to a backup. I also followed the best practices and insights from the official mongo documentation.

## Start the containers
- clone the repo https://github.com/manuel-cestaro-personal/MSSQL-Docker/archive/refs/heads/main.zip
- `cd MongoDB-Docker`
- `mkdir .secrets && cd .secrets`
- `nano mongo_user.txt` --> write the name of the mongo user
- `nano mongo_pwd.txt` --> write the pwd of the mongo user
- `cd ..`
- `docker network create <Your_Network_Name>` --> create your docker network
- `nano docker-compose.yml` --> edit the file with `<Your_Network_Name>`
- if you want edit the `docker-compose.yml` with differents paths for the `.secret` directory or the `mount bind` volumes
- `docker-compose up -d`
- use `docker ps -a` to check the containers

## Conclusions
Nothing&#128517;, this is my way of working!&#128513;<br>
It sounds simple but it took me many hours of work.<br>
Hope it can help you!&#128521;&#128406;