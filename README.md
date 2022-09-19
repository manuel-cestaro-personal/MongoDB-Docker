# MongoDB with Docker
Example of MongoDB with Docker container.<br>
References:
- https://hub.docker.com/_/mongo
- https://www.mongodb.com/compatibility/docker

## Objective
The goal is to create a MongoDB container that saves data persistently and easily copied to a backup. I also followed the best practices and insights from the official mongo documentation.

## Start the containers
- clone the repo https://github.com/manuel-cestaro-personal/MongoDB-Docker/archive/refs/heads/main.zip
- `cd MongoDB-Docker`
- `mkdir .secrets && cd .secrets`
- `nano mongo_user.txt` --> write the name of the mongo admin user ("root" usually)
- `nano mongo_pwd.txt` --> write the pwd of the mongo user
- `cd ..`
- `docker network create <Your_Network_Name>` --> create your docker network
- `nano docker-compose.yml` --> edit the file with `<Your_Network_Name>`
- if you want edit the `docker-compose.yml` with differents paths for the `.secret` directory or the `mount bind` volumes
- `docker-compose up -d`
- use `docker ps -a` to check the containers

## Access to the command line
> \# access to container command line<br />
> docker exec -it mongo bash<br />
> \# access to mongo command line; use the credentials wrote in .secret<br />
> mongosh admin -u 'username'

## Useful commands

## Setup application users
Remember that the users exist in the DB where are created. So this must be specified when you use an user different form the main admin!
> use <DB_Name><br />
> show users&nbsp;&nbsp;\# show users in the current DB<br />
> db.createUser\(<br />
> \{ user: "adminBudo3k",<br />
&nbsp;&nbsp;pwd: "StartsS0n=Z3usK1ng",<br />
>&nbsp;&nbsp;roles: \[\{role: "readWrite" , db:"Budo3k"\}\]<br />
> \}\)<br />
> show users

## Access to the DB from outside the docker network

## Conclusions
Nothing&#128517;, this is my way of working!&#128513;<br>
It sounds simple but it took me many hours of work.<br>
Hope it can help you!&#128521;&#128406;