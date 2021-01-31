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

```
