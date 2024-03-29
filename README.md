# Various-Script-of-Installation
Jenkins, Docker, Kubernetes Installation


Kubernetes Installation shell Script - 
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

***************************************************************************************************
# Docker installation shell script 
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

```

### After this script, Need to run this command to install docker. 
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```
sudo chmod 666 /var/run/docker.sock
```

# Creating Sonarqube container on Docker

```
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```

# Creating a nexus container on the nexus server
```
docker run -d --name nexus -p 8001:8001 sonatype/nexus3
```

## Jenkins Installation script 

```
#!/bin/bash
# Install OpenJDK 17 JRE Headless
sudo apt install openjdk-17-jre-headless -y
# Download Jenkins GPG key
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
 https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
# Add Jenkins repository to package manager sources
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
 https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
 /etc/apt/sources.list.d/jenkins.list > /dev/null
# Update package manager repositories
sudo apt-get update
# Install Jenkins
sudo apt-get install jenkins -y
```

## To install Trivy 

```
sudo apt install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo "deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt update
sudo apt install trivy
```

*******************************************************************************

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



