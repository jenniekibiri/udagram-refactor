# Apply env variables and secrets
kubectl apply -f aws-secret.yaml
kubectl apply -f env-secret.yaml
kubectl apply -f env-configmap.yaml
kubectl apply -f udagram-frontend.yaml
kubectl apply -f udagram-api-user.yaml
kubectl apply -f udagram-api-feed.yaml
kubectl apply -f udagram-reverseproxy.yaml

kubectl delete service reverseproxy-service  
kubectl delete service backend-feed
kubectl delete service backend-user
kubectl delete service reverseproxy 
kubectl delete service frontend

kubectl delete pod udagram-backend-user-7c47cd6688-svwsc 
kubectl delete deployment reverseproxy
kubectl delete deployment backend-feed
kubectl delete deployment backend-user



kubectl expose deployment frontend --type=LoadBalancer --name=frontend

kubectl expose deployment reverseproxy --type=LoadBalancer --name=publicreverseproxy

kubectl expose deployment backend-user --type=LoadBalancer --name=publicbackenduser
kubectl exec backend-user-b757d6668-mjg56  -c backend-user -it -- //bin//sh