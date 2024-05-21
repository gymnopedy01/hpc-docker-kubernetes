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