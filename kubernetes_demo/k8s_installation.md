# _Kubernetes installation on Ubuntu_

# On master Machine and All worker nodes
## Install Docker
*As Root*
``` bash linenums="1"
apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Install Kubernetes
*As Root*
``` bash
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
# On Master machine
## Initiate cluster
*As Root*
``` bash
kubeadm init --apiserver-advertise-address=172.31.15.121 --pod-network-cidr=192.168.0.0/16 --ignore-preflight-errors=Mem,NumCPU
```
Preserve the  `Kubeadm Join` command. example
```kubeadm join 10.128.0.22:6443 --token sdcr7n.0wrfcfpod2xvqnf3 \
    --discovery-token-ca-cert-hash sha256:562a240ede849125411def27140718e25f637071abba671823eeb1dff06b7b92
```

## Enable AutoCompletion (Optional)
``` bash
echo 'source <(kubectl completion bash)' >>~/.bashrc
source ~/.bashrc
```

## Install network
``` bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

# On All Worker Nodes
## Join cluster
*As Root*
``` bash
kubeadm join 10.128.0.22:6443 --token sdcr7n.0wrfcfpod2xvqnf3 \
    --discovery-token-ca-cert-hash sha256:562a240ede849125411def27140718e25f637071abba671823eeb1dff06b7b92
```
