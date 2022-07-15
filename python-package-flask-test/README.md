# python-package-flask-test_service.yaml

## Execute
kubectl apply -f 1-python-package-flask-test_deployment.yaml

kubectl expose deployment python-package-flask-test-deployment --type=NodePort --port=5000
kubectl port-forward service/python-package-flask-test-deployment 5000:5000
### OR
kubectl apply -f 2-python-package-flask-test_service.yaml

## Execute AZ
kubectl apply -f 3-python-package-flask-test_deployment_az.yaml
kubectl apply -f 4-python-package-flask-test_service_az.yaml
