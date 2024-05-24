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
```


https://github.com/weaveworks/weave/blob/master/site/kubernetes/kube-addon.md#-installation 



source <(kubectl completion bash)