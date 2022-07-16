# sample flask with redis

## Manually execute the app
- Must have redis installed locally
- SET REDIS_HOSTNAME=localhost
- python3 flask_app.py

## Endpoints
- localhost:5000/
- localhost:5000/set_price/<int:price>
- localhost:5000/get_price


## Build images
- docker build --tag=ricardoahumada/redis -f redis/Dockerfile .
- docker build --tag=ricardoahumada/flaskappforredis -f app/Dockerfile .

## Run images
- docker run --detach --publish=6379:6379 --name=redis ricardoahumada/redis
- docker run --detach --publish=8080:80 --name=flaskappforredis ricardoahumada/flaskappforredis

## Push images
- docker push ricardoahumada/redis
- docker push ricardoahumada/flaskappforredis

## Deploy in kubernetes
- kubectl apply -f flaskappwithredis/app-ns.yaml
- kubectl apply -f flaskappwithredis/flaskapp-svc.yaml
- kubectl apply -f flaskappwithredis/flaskapp-rs.yaml
