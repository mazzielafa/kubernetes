# GUESTBOOK EXAMPLE
## ref: https://kubernetes.io/docs/tutorials/stateless-application/guestbook/ 

## Execute
kubectl apply -f redis-leader-deployment.yaml
kubectl apply -f redis-leader-service.yaml
kubectl apply -f redis-follower-deployment.yaml
kubectl apply -f redis-follower-service.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml


## scale
- kubectl scale deployment frontend --replicas=5

## Clean
kubectl delete deployment -l app=redis
kubectl delete service -l app=redis
kubectl delete deployment frontend
kubectl delete service frontend
