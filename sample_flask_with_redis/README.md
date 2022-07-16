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
- ⚠remember stopping redis on localhost and unset ENV:
	- sudo service redis stop
	- unset REDIS_HOSTNAME
- docker run --detach --publish=6379:6379 --name=redis ricardoahumada/redis
	- ⚠Set REDIS_HOSTNAME to redis IP:
		- docker inspect container redis | more
		- export REDIS_HOSTNAME=<IP>
- docker run -d -p=5000:5000 -e REDIS_HOSTNAME=172.17.0.2  --name=flaskappforredis ricardoahumada/flaskappforredis
	- For verify start:
		- docker run -it -p=5000:5000 -e REDIS_HOSTNAME=172.17.0.2  --name=flaskappforredis ricardoahumada/flaskappforredis

## Push images
- docker push ricardoahumada/redis
- docker push ricardoahumada/flaskappforredis

## Deploy in kubernetes
- kubectl apply -f flaskappwithredis/app-ns.yaml
- kubectl apply -f flaskappwithredis/redis-rs.yaml
- kubectl apply -f flaskappwithredis/redis-svc.yaml
- kubectl apply -f flaskappwithredis/flaskapp-rs.yaml
- kubectl apply -f flaskappwithredis/flaskapp-svc.yaml

## Inspect
- kubectl get namespaces
- kubectl get all -n flaskapp-dev
- kubectl get services -n flaskapp-dev
- kubectl describe service/flaskapp -n flaskapp-dev
- kubectl get replicasets -n flaskapp-dev
- kubectl describe replicaset/flaskapp -n flaskapp-dev
- kubectl get deployments -n flaskapp-dev


## Clean up
- kubectl delete service flaskapp -n  flaskapp-dev
- kubectl delete replicaset flaskapp -n flaskapp-dev
- OR all in all:
	- kubectl delete all --all -n flaskapp-dev

