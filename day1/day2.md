ipc (인터프로세스콜) 는 ipcs 명령어로 확인가능
uid /etc/passwd 여기에 저장


# Union File System
Union Mount Filesystem
Layered File System
Overlay fileSystem(Overlay FS 2)
```aufs / devicempper / ...```


OHP (Overhead Projector 처럼 필름을 올려서 사용하는 컨셉

윈도우의경우 드라이브레터 c: d:
유닉스의경우 하나의 파일시스템에 루트를 지정하여 사용

말이 있고 그거에 올라타는 것과 비슷하여 마운트라고함 (마운트라는 명령어로 확인 가능함 ) 
마운트 해제 명령어
```$ umount```


파일의 구조 : 
파일시스템의 구조 :
마운트의 구조 : 파일시스템들을 엮어서 큰 루트 파일 시스템을 만드는것


도커의 경우 아래는 readonly , 맨위만 wrtieable 가능한 레이어 구조로 함

컨테이너는 업데이트와 배포에 유리한 구조임


도커 설치
``` sh
wget -qO- https://get.docker.com | sh -
```

ssh 설치
``` sh
sudo apt install openssh-server

sudo systemctl enable ssh --now ssh
sudo systemctl status ssh
sudo ufw status         //firewall 검사
ssh kcia@localhost      
```

hostname 세팅
``` sh
hostnamectl set-hostname --static k8s-21-1
```

docker는 root 와 docker 그룹에서 실행 가능한걸로 확인된다.
``` sh
type docker 
ls -l /usr/bin/docker
```

유닉스 도메인 소켓으로 만들어짐. 파일시스템임. 소켓 파일인걸 확인하자
``` sh
ls -l /var/run/docker.sock
srw 의 s는 소켓파일임
```

kcia 유저는 루트도 아니고, 도커유저도 아니기때문에  접근이 불가함.
루트로 접근하거나, docker 그룹을 부여하는방법
``` sh
tail /etc/group
sudo usermod -aG docker kcia
tail /etc/group
id
```

/etc/hosts 추가
``` sh
sudo vi /etc/hosts
#아래 라인 추가한다.
10.100.152.151 k8s-21-1
10.100.152.152 k8s-21-2
```

도커 스왑을 꺼주는게 좋다.
``` sh
cat /proc/swaps
swapoof -a
sudo vi /etc/fstab 
# swapfile 주석 처리한다
```

리눅스 재시작!

설치 확인하기
``` sh
ip a
id
cat /proc/swaps
docker version
ls -l car/run/docker.sock
```




# Docker
1. Docker Host /server /Engine
2. Docker Client
3. Registry




