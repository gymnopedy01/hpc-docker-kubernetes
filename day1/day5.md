#

![교육장](../교육장-네트워크-구성환경.png)


데몬셋  
모든 노드에 한개씩 떠야함

라이브니스프로브를 따로 안주면
pid 1 번으로 판단함

kube-proxy 는 넷필터를 통해 cni 통신 실패난걸 K8S 서비스리소스에 있는지 확인해서 레코드를 확인해서 응답해줌


드레인
노드에 더이상 스케쥴링 하지 않도록 알려줌

delete node


ls /var/lib/kubelet  
임시데이터 만들었던 흔적이이음

ls /var/lib/conainerd  


실습. 초기화후 위브넷 설치
```
sudo kubeadm reset

kubeadm init --pod-network-cidr 10.32.0.0/12

alias k=kubectl
k api-resources


sudo ctr image ls
sudo ctr image pull docker.io/weaveworks/weave-kube:latest
sudo ctr image pull docker.io/weaveworks/weave-npc:latest
```

kubectl get ds --all-namespaces


https://github.com/weaveworks/weave/blob/master/site/kubernetes/kube-addon.md#-installation 

kubecl delee pods weavene-sadf-

source <(kubectl completion bash)



```sh

kubeadm init --pod-network-cidr 10.10.0.0/16

```

kubectl -f pod.yml
ip route 

kubectl por-forward hello-pod 5000:8000


replicaset
매치레이블값과 파의 레이블의 갑은 같아야한다.


deployment
버전1 버전2 이렇게 레플리카셋간의 롤아웃 롤백을 해준다.
