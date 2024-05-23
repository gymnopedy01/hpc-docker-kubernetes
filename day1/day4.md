팟안에 컨테이너가 있고 , 컨테이너는 여러가지 컨테이너가 있을수 있음.


여러개의 컨테이너가 뜰 수 있음
helper conainer , support conainer


팟은 기본적으로 호스트하고 네트워크는 격리시킴

컨테이너가 뜨면 pid, 파일시스템은 컨테이너 단위로 격리



오버레이 네트워크의 vxlan gre 프로토콜

팟은 호스트는 하ㅏ 네트워크 하나로 생각


repica set 이 새로 나온 이유
replicaioncontroller 로는 deployment를모만들어서 새로 만듬

롤아웃
 새버전 구버전 배포후 트래픽을 변경하는거

 https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.30/


# Services
DNS 호스트 네임 역할을 해줌


서비스 자원을 만들고 ,  팟 내부에서는 서비스이름으로 접근
쿠베프로기가 레이블을 보고 결정함
보내는건 cni 플러그인들이 하는거


Play With Kubernetes

Insalling kube adm
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
https://www.cherryservers.com/blog/install-kubernetes-on-ubuntu 


Installing Kubernetes
```sh

cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

sudo sysctl --system
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo mkdir /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

sudo sh -c "containerd config default > /etc/containerd/config.toml"
sudo sed -i 's/ SystemdCgroup = false/ SystemdCgroup = true/' /etc/containerd/config.toml

sudo systemctl restart containerd.service
sudo systemctl restart kubelet.service
sudo systemctl enable kubelet.service
```

```sh
sudo kubeadm config images pull
sudo kubeadm init --pod-network-cidr=10.10.0.0/16

초기화 는
sudo kubeadm reset
sudo kubeadm init

설치완료되면 worker 노드에ㅓ
kubeadm join 10.100.152.111:6443 --token pfdyn9.23d9hzsly6xnfdlp \
        --discovery-token-ca-cert-hash sha256:15c18ed06c6923211e3833035d00cee8c6fb95e86cc9a7f41563764722dd7d8c

kubectl get node

```


Addon 설치
Installaion Calico
```sh
https://docs.tigera.io/calico/latest/getting-started/kubernetes/quickstart#:~:text=Install%20Calico%201%20Install%20the%20Tigera%20Calico%20operator,node%20in%20your%20cluster%20with%20the%20following%20command.


kcia@k8s-1-1:~$ kubectl get pod --all-namespaces -o wide
NAMESPACE         NAME                               READY   STATUS    RESTARTS        AGE     IP               NODE      NOMINATED NODE   READINESS GATES
kube-system       coredns-7db6d8ff4d-4cncq           0/1     Pending   0               64m     <none>           <none>    <none>           <none>
kube-system       coredns-7db6d8ff4d-77h2s           0/1     Pending   0               64m     <none>           <none>    <none>           <none>
kube-system       etcd-k8s-1-1                       1/1     Running   0               69m     10.100.152.111   k8s-1-1   <none>           <none>
kube-system       kube-apiserver-k8s-1-1             1/1     Running   0               69m     10.100.152.111   k8s-1-1   <none>           <none>
kube-system       kube-controller-manager-k8s-1-1    1/1     Running   7 (5m21s ago)   69m     10.100.152.111   k8s-1-1   <none>           <none>
kube-system       kube-proxy-d4mbl                   1/1     Running   0               64m     10.100.152.111   k8s-1-1   <none>           <none>
kube-system       kube-proxy-r7qsx                   1/1     Running   0               24m     10.100.152.112   k8s-1-2   <none>           <none>
kube-system       kube-scheduler-k8s-1-1             1/1     Running   7 (6m26s ago)   69m     10.100.152.111   k8s-1-1   <none>           <none>
tigera-operator   tigera-operator-76ff79f7fd-bwc7p   1/1     Running   0               5m49s   10.100.152.112   k8s-1-2   <none>           <none>


```




