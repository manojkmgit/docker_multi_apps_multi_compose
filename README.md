# create the network before running docker-compose up on the projects included in this repo
docker network create --driver=bridge mynet

# go to these individual dirs and run:
cd redis
docker-compose up

# get the ip of the redis app
docker network inspect mynet

look for something like "IPv4Address": "172.21.0.3/16" for redis container
then 172.21.0.3 is the IP of redis app

# put redis app IP in flasl code file app.py
cd ../flask
vi app.py
here
put/replace with:
cache = redis.Redis(host='172.21.0.3', port=6379)

# start flash app container
docker-compose up

it will show the IP where flask app is running

