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
> \# show the created databases; don't delete default dbs<br />
> show dbs<br />
> \# with the same command you can chance workin db or create a new db<br />
> use <DB_Name><br />
> \# delete the current db<br />
> db.dropDatabase()<br />
> \# creare a collection for the current db<br />
> db.createCollection(<Collection_Name>)<br />
> \# show collections for the current db<br />
> show collections<br />
> \# delete a specific collection for the current db<br />
> db.<Collection_Name>.drop()<br />

&#9888; A database without a collection will be automatically delete!

## Setup application users
Remember that the users exist in the DB where are created.<br />
So this must be specified when you use an user different form the main admin!
> use <DB_Name><br />
> show users&nbsp;&nbsp;\# show users in the current DB<br />
> db.createUser\(<br />
> \{ user: "<User_name>",<br />
&nbsp;&nbsp;pwd: "<Pass_word>",<br />
>&nbsp;&nbsp;roles: \[\{role: "readWrite" , db:"<DB_Name>"\}\],<br />
>&nbsp;&nbsp;mechanisms: [ "<SCRAM-SHA-1|SCRAM-SHA-256>" ]&nbsp;&nbsp;&nbsp;&nbsp;\# The default is both SCRAM-SHA-1 and SCRAM-SHA-256.<br />
> \}\)<br />
> show users

## Access to the DB from outside the docker network
In the compose file you can see a volume that point to the file `mongod.conf.orig`. This is the configuration file of MongoDB and editing it you can quicly permit or deny the access to the container from the server port.<br />
Edit as follow:
>\# network interfaces<br />
>net:<br />
>&nbsp;&nbsp;port: 27017<br />
>&nbsp;&nbsp;bindIp: 127.0.0.1,<Server_IP><br />

In this way you can access from a GUI as **MongoDB Compass**: https://www.mongodb.com/it-it/products/compass<br />
Use a connection string as:<br />
`mongodb://<username>:<pwd>@<server_ip>:27017/?authMechanism=DEFAULT&authSource=<DB_Name>`

## Conclusions
Nothing&#128517;, this is my way of working!&#128513;<br>
It sounds simple but it took me many hours of work.<br>
Hope it can help you!&#128521;&#128406;
