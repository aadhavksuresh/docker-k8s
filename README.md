[![HitCount](http://hits.dwyl.io/akasranjan005/docker-k8s.svg)](http://hits.dwyl.io/akasranjan005/docker-k8s)

# Docker & K8s

1  [Docker Installation](#1-docker-installation---documentation)  
2  [Docker-Compose Installation](#2-docker-compose-installation---documentation)  
3  [Installing Kubernetes](#3-installing-kubernetes---documentation)  
    3.1  [Ubuntu](#31-ubuntu)  
    3.2  [CentOs](#32-centos)  

## 1. Docker Installation - [Documentation](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce)

### 1.1 Ubuntu
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"
sudo apt-get update
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu
sudo apt-mark hold docker-ce
```

### 1.2 CentOs

```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce
```


## 2. Docker-Compose Installation - [Documentation](https://docs.docker.com/compose/install/#prerequisites)

```
sudo curl -L https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


## Blog
You can ready my blog on docker [here](https://blogs.akashranjan.in)

## 3. Installing Kubernetes - [Documentation](https://kubernetes.io/docs/setup/)

### 3.1 Ubuntu

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

create a file /etc/apt/sources.list.d/kubernetes.list
```
cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

Update the packages
```
sudo apt update
```

Install Kubernetes
```
sudo apt-get install -y kubelet=1.18.0-00 kubeadm=1.18.0-00 kubectl=1.18.0-00
sudo apt-mark hold kubelet kubeadm kubectl
```

Add the iptables rule to sysctl.conf:

```
echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf
```

Enable iptables:

```
sudo sysctl -p
```

Initialize the cluster (run only on the master):

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

Set up local kubeconfig (run only on the master):

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Join nodes with master. Run below command on nodes

```
kubeadm join <MASTER_NODE_IP>:6443 --token <TOKEN> \
    --discovery-token-ca-cert-hash <HASH>
```


Install Flannel CNI (run only on the master)
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

* Additional Configs
```
ToDO
```

### 3.2 CentOs

```
ToDo
```

```

* Install Kubernetes Dashboard

```
ToDo
```

* ToDo:
  * Add Sample Dockerfile and docker-compose file and explanation
  * Add kubernetes sample file and explanation 
