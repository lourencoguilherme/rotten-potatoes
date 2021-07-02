###Build image python
````

1 - Faça um build da imagem
dentro da pasta rotten-potatoes/src
docker build -t gu1lh3rm/rotten-potatoes:v1 .

2 - gerar uma tag latest e enviar para o docker hub
docker tag gu1lh3rm/rotten-potatoes:latest gu1lh3rm/rotten-potatoes:v1
docker push gu1lh3rm/rotten-potatoes:latest
docker push gu1lh3rm/rotten-potatoes:v1

3 - criar um cluster para aplicações e fazer um bind para o loadbalancer
k3d cluster create clusterrottenpotatoes --servers 1 --agents 2 -p "8080:30000@loadbalancer"
kubectl get nodes

4 - Criar o k8s para o banco de dados mongo db
kubectl apply -f k8s/mongodb/deployment.yaml
kubectl get pods
kubectl get nodes
kubectl get deployments
kubectl get all

5- Criar o services em k8s mongodb
kubectl apply -f k8s/mongodb/service.yaml
kubectl get services
kubectl get all

6 - Criar o deployment
kubectl apply -f k8s/web/deployment.yaml
kubectl get pods

````