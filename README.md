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
#  kind create cluster 
k8s_version='1.14.3'
cat <<EOF | kind create cluster --image kindest/node:v${k8s_version} --name sanjay  --config=-
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
EOF


# K9s Kubectl cli
wget https://dl.google.com/go/go1.15.2.linux-amd64.tar.gz
sudo tar -C /usr/local -xf go1.15.2.linux-amd64.tar.gz
$ vim ~/.bash_profile
export PATH=$PATH:/usr/local/go/bin
Then get the file to keep the configuration.
source ~/.bash_profile
In order to build K9 from source, you must clone the repository before proceeding.
cd ~
git clone https://github.com/derailed/k9s.git
cd ~/k9s

Build and run the executable file
$ make build && ./execs/k9s


# Load balancer MetalLB 

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


# Ingress controller ISTIO  1.8.2
curl -L https://istio.io/downloadIstio | sh -

## Default install 
cd istio*
istioctl operator init
istioctl install
## Default install 

kubectl create namespace istio-system
helm install -n istio-system istio-base manifests/charts/base
helm install --namespace istio-system istiod manifests/charts/istio-control/istio-discovery \
    --set global.hub="docker.io/istio" --set global.tag="1.8.2"

kubectl get pods -n istio-system -w 

kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.8/samples/addons/kiali.yaml
kubectl -n istio-system get svc kiali



kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml

kubectl get api-services 
kubectl get api-resources 

# Service deploy on cluster 

kubectl create deployment nginx --image=nginx:1.16-alpine  -o yaml --dry-run
kubectl create deployment nginx --image=nginx:1.16-alpine 
kubectl expose deploy nginx --port=80 --type LoadBalancer  
kubectl get svc -owide   
kubectl expose deploy nginx --port=80 --type NodePort 

Install nginx in VM 
config 172 to the load balancer kubernetes ti metallb
server {
  listen 80;
  location / {
  proxy_pass http://172.18.255.200 ;
  }
}


kubectl create deployment webapp --image=caddy:2.2.1-alpine 
kubectl expose deploy webapp --port=80 --type LoadBalancer  
kubectl get svc -owide   


Kubernetes Dashoard 
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml




```
https://www.sohamkamani.com/blog/2016/11/22/docker-server-busybox-golang/
