# WORPRESS SERVICE
 
## Create
kubectl apply -k ./

## Inspect
kubectl get secrets

kubectl get pvc

kubectl get pods

kubectl get services wordpress

minikube service wordpress --url

## Delete/clean
kubectl delete -k ./
