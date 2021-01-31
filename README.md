# Kubernetes-KinD

## Ubuntu 

```
 apt install docker.io 
 curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.10.0/kind-linux-amd64
 chmod +x ./kind
 mv ./kind /usr/bin/kind

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod 755 kubectl ; mv kubectl /usr/bin/

wget https://get.helm.sh/helm-v3.5.1-linux-arm64.tar.gz
tar xvf helm* 
mv linux-arm64/helm /usr/bin 

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

cp /usr/local/bin/helm /usr/bin/helm 

# docker pull kindest/node:v1.14.3
kind create cluster 

Load balancer MetalLB 

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/master/manifests/namespace.yaml
kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)" 
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/master/manifests/metallb.yaml
kubectl get pods -n metallb-system --watch

docker network inspect -f '{{.IPAM.Config}}' kind

echo 'apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 172.18.255.200-172.19.255.250 '   > metallb.yaml 

kubectl apply -f metallb.yaml 


```
