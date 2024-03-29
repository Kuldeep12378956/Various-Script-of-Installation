# Various-Script-of-Installation
Jenkins, Docker, Kubernetes Installation


Docker Installation shell Script - 
```
sudo apt-get update
sudo apt install docker.io -y
sudo chmod 666 /var/run/docker.sock
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

```
Note :- After this done, Need to run comman 4 & 5 on master and slave & command 6 need to be run on Master only





# 1 to install Docker  & Kubernetes -

```
sudo apt-get update
```

# 2 Installing Docker - 
```
sudo apt install docker.io -y
sudo chmod 666 /var/run/docker.sock
```

# 3 Installing required dependenies of kubernetes on Master and slaves
```
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
sudo mkdir -p -m 755 /etc/apt/keyrings
```
#Adding Kubernetes repository and GPG key on master and slave
```
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

```
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
*****************************************************************************

# 4 Update Package list on master and node. 

```
sudo apt update
```

# 5 Install Kubernetes Components[On Master & Worker Node]

```
sudo apt install -y kubeadm=1.28.1-1.1 kubelet=1.28.1-1.1 kubectl=1.28.1-1.1
```

# 6 Initialize Kubernetes Master Node [On MasterNode]

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

```

# 6 Configure Kubernetes Cluster [On MasterNode]

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

```

# 7 Deploy Networking Solution (Calico) [On MasterNode]
```
kubectl apply -f https://docs.projectcalico.org/v3.20/manifests/calico.yaml
```

# 8 Deploy Ingress Controller (NGINX) [On MasterNode]
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
```

## After all this done we need to scan the kubernetes cluster with some tool and that tool is kubeaudit.  which can be downloaded from below link. 

```
https://github.com/shopify/kubeaudit/releases

```
After downloading we need to extract the tar file, > Move the kube audit file to the locatoion /usr/local/bin > then run command 'kubeaudit all'

```
mv kubeaudit /usr/local/bin
```
```
kubeaudit all
```


