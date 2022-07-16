# sample flask with redis

## Manually execute the app
- ⚠Must have redis installed locally!
	- sudo apt update
	- sudo apt install -y redis-server
	- sudo service redis status
- Set env REDIS_HOSTNAME
	- Windows: 
		- SET REDIS_HOSTNAME=localhost
	- Linux: 
		- export REDIS_HOSTNAME=localhost
- python3 flask_app.py

## Endpoints
- curl localhost:5000/
- curl localhost:5000/set_price/<int:price>
	- example: curl localhost:5000/set_price/2346
- curl localhost:5000/get_price


## Build images
- docker build --tag=ricardoahumada/redis -f redis/Dockerfile .
- docker build --tag=ricardoahumada/flaskappforredis -f app/Dockerfile .

## Run images
- ⚠remember stopping redis on localhost:
	- sudo service redis stop
- docker run --detach --publish=6379:6379 --name=redis ricardoahumada/redis
- docker run --detach --publish=8090:80 --name=flaskappforredis ricardoahumada/flaskappforredis

## Push images
- docker push ricardoahumada/redis
- docker push ricardoahumada/flaskappforredis

## Deploy in kubernetes
- kubectl apply -f flaskappwithredis/app-ns.yaml
- kubectl apply -f flaskappwithredis/flaskapp-svc.yaml
- kubectl apply -f flaskappwithredis/flaskapp-rs.yaml
