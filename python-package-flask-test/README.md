# APP: python-package-flask-test 

## Execute Normal:
### Deployment:
	- kubectl apply -f 1-python-package-flask-test_deployment.yaml
	- kubectl logs deployment/python-package-flask-test-deployment
### Service:
	- Manually:
		- kubectl expose deployment python-package-flask-test-deployment --type=NodePort --port=5000
	 	- kubectl port-forward service/python-package-flask-test-deployment 5000:5000
 	- Using yaml:
		- kubectl apply -f 2-python-package-flask-test_service.yaml
		- kubectl port-forward service/python-package-flask-test-service 5000:5000
	- Consume:
		- curl localhost:5000/api/v1/restricted

### Clean up
	- kubectl delete service python-package-flask-test-service
	- kubectl delete deployment python-package-flask-test-deployment

## Execute AZ: same as Normal, but...
- ⚠Needs AZ credentials to be added to kubectl:
	- Login into azure registry:
		- docker login [acr-path]
	- Add credentials to kubectl:
		- kubectl create secret generic acr-secret --from-file=.dockerconfigjson=$HOME/.docker/config.json --type=kubernetes.io/dockerconfigjson
- kubectl apply -f 3-python-package-flask-test_deployment_az.yaml
- kubectl apply -f 4-python-package-flask-test_service_az.yaml
- kubectl port-forward service/python-package-flask-test-service-az 5000:5000

### Clean up AZ
	- kubectl delete service python-package-flask-test-service-az
	- kubectl delete deployment python-package-flask-test-deployment-az

## Deploy into Azure AKS cluster
- ⚠Needs AZ cluster:
	- https://docs.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal?tabs=azure-cli
- ⚠Needs AZ installation:
	- curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
	- ref: https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli
	- az login
	- az aks get-credentials --resource-group [myResourceGroup] --name [myAKSCluster] --admin
- kubectl config get-contexts
- kubectl config set current-context AZ-CONTEXT
- kubectl get nodes

### Clean up
	- az logout
	- kubectl config set current-context minikube
