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

*If* you have any current containers on the same ports, the proxy may not work. To prevent that do:
`docker-compose down`

Then build the docker containers:
`docker-compose up`
You will see 3 containers spin up, first the app containers and then the nginx container.

Navigate to `localhost:8080/static/cat-typing.gif` to see the a fun cat GIF! Or `localhost:8080/static/it_crowd_meme.jpg` for any IT crowd fans :P. This is doing the routing to a static page.

If you navigate to `localhost:8080`, you should see a greeting from App 1. Do a hard refresh `CMD + r` and you should see a greeting from App 2. This is the NGINX server doing load balancing using the round robin rule.

When doing the requests above, we can see the logs in the running containers. The logs are custom and can be made more readable using `jq`. Install jq via:
`brew install jq`

To prettify the logs we can do:
`echo '{"timestamp":"2019-02-25T04:41:55+00:00","msec":"1551069715.451",...}' | jq`

Voila!
