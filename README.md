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

6 - Criar o deployment da aplicação web
kubectl apply -f k8s/web/deployment.yaml
kubectl get deployments

7 - Criar o service de aplicação web
kubectl apply -f k8s/web/service.yaml
kubectl get services

8 - aplicação web sobe em
http://localhost:8080/
http://localhost:8080/host -- lista pods

9 - escalar pods de forma rapida
kubectl scale deployment movies --replicas 10

kubectl delete all --all --all-namespaces

````


###Build git CI/CD
````

doctl kubernetes cluster kubeconfig save 741ca32d-1944-4b94-bac1-d6860493dc9f

cd ~/.kube && kubectl --kubeconfig="k8s-aula-kubeconfig.yaml" get nodes

cp k8s-aula-kubeconfig.yaml ~/.kube/config

````