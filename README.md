This example shows how separate containers can interact over the user created network using the container name itself, rather than any need to hard code the IPs.

# create the network before running docker-compose up on the projects included in this repo
docker network create --driver=bridge mynet

# go to these individual dirs and run:
cd redis
docker-compose up --build

# get the ip of the redis app
docker network inspect mynet

look for something like "IPv4Address": "172.21.0.3/16" for redis container
then 172.21.0.3 is the IP of redis app

# put redis app IP in flask code file app.py
cd ../flask
vi app.py
#put/replace with:
cache = redis.Redis(host='172.21.0.3', port=6379)

or use just the name of the redis container

cache = redis.Redis(host='redis_host', port=6379)

# start flash app container
docker-compose up --build

docker-compose ps

curl http://localhost:5001

It should work.

