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



```
