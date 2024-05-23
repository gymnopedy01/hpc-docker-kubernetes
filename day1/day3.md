# Docker Theory of Operation

## Using Docker

https://docs.docker.com/engine/reference/commandline/docker/
```sh
$ docker <subcommand> <arg>
$ docker <mgmtcommand> <subcommand> <arg>
```

-mgmt command
 > builer/checkpoint/config/container/image/network node/plugin/secret/service/stack/swarm system/trust/volume

version1 스타일 명령어
```sh
docker search #이미지 찾기
docker ps #v2 의 docker container ls 와 동일
docker rm #컨테이너 정보 지우기
docker rmi #이미지 정보 지우기 
```

sample : https://hub.docker.com/_/registry

```sh
$ docker run -d -p 5000:5000 --restart always --name registry registry:2
-p 포트 앞에꺼 호스트:뒤에껀 컨테이너 
--restart 1번 프로세스가 죽으면 리스타트
--name registry 이름을 명시적으로 registry로 지어줌
registry:2 이미지 registry 2번 버전으로 가져옴
```
ex. image) 
myhost.mycompany.com:5000/ubuntu:14.04

컨테이너 네트워크  
  컨테이너간 통신을 하려면 오버레이네트웍이 필수임
  파드네트워크 = 컨테이너네트워크 = 오버레이네트워크 비슷한 말임

오버레이네트워크는 L3 L2 인켑슐레이트 기술

쿠버네티스에서는 다 구현할수 없어서 스펙만 정의하고 container network interface (CNI) 라고 부른다! . 잘하는 업체에 믿고 맡겨!



What is Kubernetes
- Feature 
  - An orchestrator of conainerized apps
Supports scaling, self-healing, load-balancing, rolling update, etc
History

https://kubernetes.io/


디자이어드 스테이트가 벗어나면 힐링, 워크로드가 많아지면 스케일링, 오토메이션

Horizontal scaling은 시스템에 노드를 추가하거나 제거하여 숫자를 조정하는 scale out/in을 의미합니다.
vertical scaling 스펙을 늘리는 스케일링 scale up/down

CRI Container Runtime Interface

containerd가 만들어진 배경은
oci(Open container initiative) 때문에 만들어짐. containerd가 다시 만든게 도커 



https://kubernetes.io/blog/2018/05/24/kubernetes-containerd-integration-goes-ga/



Cloud Native computing


Youtube - Google I/O 2014 - Containerizing the Cloud with Docker on Google Cloud Platform
https://www.youtube.com/watch?v=tsk0pWf4ipw



발빠르게 스케일아웃, 
B2C에 더 적합함. B2B보다는 

변화의속도에 맞게끔 



마스터
 컨트롤 플레인이라고도 불렸음
 API 서버가 구동되고 있음

노드
 쿠블릿이 구동되고 있음. 
 컨테이너런타임(container runtime, docker, ciro))이 있음 


쿠버네티스 명령은 
- 우리 컨테이는 이 모양으로 떠있게 해주세요. 점잖게 얘기함 . 결과만 얘기하면됨
- manifest파일은 yaml, json을 지원하며 내부에서는 json으로 통신함. 쓰기엔 yaml 이 편함
- 장애에 대한대처가 가능, 변경에 대한 대응 가능
  - actualstate 가 바뀌는건 장애.
  - desredstate 가 바뀌는건 변경.


- kubelet 은 리눅스 서비스 프로세스임
- container runtime 리눅스 서비스프로세스
- kube-proxy 컨테이너 내에 포함됨


considering for large clsuters
최대 노드는 5000개


Considerations for large clusters
A cluster is a set of nodes (physical or virtual machines) running Kubernetes agents, managed by the control plane. Kubernetes v1.30 supports clusters with up to 5,000 nodes. More specifically, Kubernetes is designed to accommodate configurations that meet all of the following criteria:

No more than 110 pods per node
No more than 5,000 nodes
No more than 150,000 total pods
No more than 300,000 total containers
You can scale your cluster by adding or removing node

https://kubernetes.io/docs/setup/best-practices/cluster-large/



api server가 kubelet들을찾아다니지않음 (5000개를 일일이 찾아 다니지 않아도됨)

kubelet들이 칠판에 일거리를 찾아옴

api server가 kubelet을 찾아가는ㄱ ㅕㅇ우는 문제가생겼ㅇㄹ경우만 빼고는 없음


``` sh 
sudo apt update 
sudo apt install -y qemu-guest-agent

ip a
sudo hostnamectl set-hostname --static k8s-1-1
sudo hostnamectl set-hostname --static k8s-1-2

sudo vi /etc/hosts
10.100.152.111 k8s-1-1
10.100.152.112 k8s-1-2

sudo vi /etc/fstab
#/swapfile                                 none            swap    sw              0       0

sudo systemctl disable systemd-resolved.service
sudo systemctl stop systemd-resolved

sudo vi /etc/NetworkManager/NetworkManager.conf
dns=default

sudo rm /etc/resolv.conf

sudo systemctl restart NetworkManager.service
cat /etc/resolv.conf


wget -qO- https://get.docker.com | sh -
```