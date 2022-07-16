# APP: python-package-flask-test 

## Execute Normal:
- Deployment:
	- kubectl apply -f 1-python-package-flask-test_deployment.yaml
	- kubectl logs deployment/python-package-flask-test-deployment
- Service:
	- Manually:
		- kubectl expose deployment python-package-flask-test-deployment --type=NodePort --port=5000
	 	- kubectl port-forward service/python-package-flask-test-deployment 5000:5000
 	- Using yaml:
		- kubectl apply -f 2-python-package-flask-test_service.yaml
		- kubectl port-forward service/python-package-flask-test-service 5000:5000
	- Consume:
		- curl localhost:5000/api/v1/restricted

## Clean up
- kubectl delete service python-package-flask-test-service
- kubectl delete deployment python-package-flask-test-deployment

## Execute AZ: same as Normal, but...
- kubectl apply -f 3-python-package-flask-test_deployment_az.yaml
- kubectl apply -f 4-python-package-flask-test_service_az.yaml
- kubectl port-forward service/python-package-flask-test-service-az 5000:5000

## Clean up AZ
- kubectl delete service python-package-flask-test-service-az
- kubectl delete deployment python-package-flask-test-deployment-az
