### NGINX proxy
The proxy does two things currently:
1. Routes to a static page displaying a gif
2. Acts as a load balancer between 2 apps, follows the round robin rule

#### Running the server

##### Pre-requisites
Need to have docker and docker-compose installed. Refer to the [docker docs](https://docs.docker.com/install/) for installation help.

##### Commands
Clone this repo:
`git clone https://github.com/bhargysh/opsinator.git`

Go into the repo:
`cd opsinator`

*If* you have any current containers on the same ports, the proxy may not work. To prevent that we can do:
`docker-compose down`

Then build the docker container:
`docker-compose up`
You will see 3 containers spin up, first the app containers and then the nginx container.

Navigate to `localhost:8080` and you should see the NGINX homepage
You can now navigate to `localhost:8080/static/cat-typing.gif` to see the a fun cat GIF! This is doing the routing to a static page.

Navigate to `localhost:3000` to see a greeting from app1, do a hard refresh `CMD + r` and you should see a greeting from app2. This is the load balancing that the NGINX server is doing.

Voila!