# ***Criação de clusters Kubernetes***

## Para iniciar a criação de clusters Kubernetes é necessário fazer a instalação do Kind. O Kind é uma ferramenta para executar clusters Kubernetes locais usando "nodes" de contêiner do Docker.


## *Para instalar o Kind no Linux utilize estes comandos*:

```

curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.9.0/kind-linux-amd64

chmod +x ./kind

mv ./kind /some-dir-in-your-PATH/kind

```

## *Após installar o Kind será possível criar um cluster local utilizando o seguinte comando:*

```
./kind create cluster --name nomedocluster
```

## *Caso haja algum erro ao criar o cluster, tente autorizar o uso do docker fora da root. Utilize os comandos abaixo:*

```
sudo groupadd docker

sudo usermod -aG docker $USER

newgrp docker 

docker run hello-world
```
## *Após a criação do seu cluster devemos instalar o Apache Ni-Fi. Utilizaremos o Helm, que é uma ferramenta para gerenciamento de pacotes para o Kubernetes. Para adicionar o repositório Helm utilize:*
```
helm repo add cetic https://cetic.github.io/

helm-charts

helm repo update
```
## *Agora installe o NiFi utilizando o Helm:*
```
helm install my-release cetic/nifi
```

## *Finalizado todo o processo acima, precisamos conseguir nos comunicar com o Kubernets, para isso é necessário installar o "kubetcl". Utilize o comando:*
```
sudo snap install kubectl --classic
```

## *Para iniciar de fato a orquestração e gerenciamento de containers precisamos antes de mais nada entender os recursos Kubernets:*

* **StatefulSet**: controlador que ajuda a implantar e dimensionar grupos de pods do Kubernetes;
* **Deployment**: objeto de recurso no Kubernetes que fornece atualizações declarativas para aplicações;
* **Services**: permite a comuniação entre componentes dentro e fora da aplicação(front-back, end-users);
* **Pod**: um conjunto de um ou mais containers implantados em um nó, sendo este o menor e mais simples objeto do Kubenets;
* **Namespaces**: cluster virtual usado para gerenciar vários clusters físicos.

## *Alguns exemplos de comandos utilizados para orquestrar e gerenciar os clusters:*
 * **kubectl get namespaces**: retorna todos os namespaces;
 * **kubectl create namespace mundodocker**: cria um namespace chamado mundodocker;
 * **kubectl get all**: retorna informações sobre o cluster;
 * **kubectl delete ns mundodocker**: delete namespace chamado mundodocker;
 * **kubectl apply (-f nome_da_pasta | -k diretorio)**: Criar ou atualizar recursos.

 ## *Para fazer a instalção do NiFi em nosso cluster devemos utilizar os seguintes comandos*:

```
helm uninstall my-release

helm install --namespace nomedonamespace my-release cetic/nif
```

# REFERÊNCIAS:

* https://kubernetes.io/docs/concepts/services-networking/service/;

* https://kubernetes.io/docs/reference/kubectl/cheatsheet/;

* https://medium.com/@maths.nunes/o-que-%C3%A9-o-helm-e-porque-voc%C3%AA-deve-us%C3%A1-lo-508b7350dcd;

* https://www.redhat.com/pt-br/topics/containers/what-is-kubernetes;
