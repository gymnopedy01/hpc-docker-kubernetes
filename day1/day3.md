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
docker search 이미지찾기
docker ps #v2 의 docker container ls 와 동일
docker rm 컨테이너 정보 지우기
docker rmi 이미지 정보 지우기 
```

sample : https://hub.docker.com/_/registry

```sh
$ docker run -d -p 5000:5000 --restart always --name registry registry:2
-p 포트 앞에꺼 호스트:뒤에껀 컨테이너 
--restart 1번 프로세스가 죽으면 리스타트
--name registry 이름을 명시적으로 registry로 지어줌
registry:2 이미지 registry 2번 버전으로 가져옴
```

myhost.mycompany.com:5000/ubuntu:14.04

컨테이너 네트워크  
  컨테이너간 통신을 하려면 오버레이네트웍이 필수임
  파드네트워크 = 컨테이너네트워크 = 오버레이네트워크

오버레이네트워크 L3 L2 인켑슐레이트 기술

쿠버네티스에서는 다 구현할수 없어서 스펙만 정의하고 container network interface (CNI) 라고 부른다! . 잘하는 업체에 믿고 맡겨!

