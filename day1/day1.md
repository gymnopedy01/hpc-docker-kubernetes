
## 메인프레임 컴퓨터
- 배치잡
- MULTICS -> UNIX 

##  OS 구조에 대한 두가지 관점
- 어플리케이션
- 쉘
- 커널
 - 
 ```
 a=a+1                      // 커널 접근 없음
 printf("HelloWorld");      // 커널 접근
 ```
 BUSY
  USER MODE : 유저가 실행
  SYSTEM MODE : 커널에서 실행
 IDLE

시스템 콜 : 

- 운전 면허 : 전기자동차면허, 내연기관자동차면허 따로있지 않다. 인터페이스 동일하기 때문
- POSIX : `Portable Operating System not unix ` 인터페이스에 대한 표준
- firm ware : 하드웨어가 제공해, 근데 소프트웨어야.  그래서 하드웨어와 커널 사이에 위치

```
/dev/eth0
리눅스는 모든디바이스가 파일 같음 그래서 폴더에서 접근해서 디바이스 읽고 씀
```

amd64 표준 정식 명칭
x86_64는 표준정식명칭의 alias


## 가상化 (visualization)
ex) 데이터센터 가상화, 스토리지, 네트워크, 메모리
물리적인 자원 (physical resources) -> 논리적인 자원 으로 만드는것을 가상화 라고 한다.

물리적인자원
 : 고정된형태/정해지 크기/ 재구성하기 어렵다
논리적인 자원?
 : 고정되어 있지 않은 형태/ 재구성할수 있는/크기 가변적

 장점(pros)
 - 자원구성에 대한 유연성 확보
 - utilization 을 높 일 수 있다
 - cost saving 가능
 - software define 가능 -> 자동화및 기타 소프트웨어 확장 가능

 단점(cons)
 - layer 증가 -> complexity 증가
 - 관리 포인트 증가
 - 애플리케이션 성능이 저하됨

응답시간 과 대여폭
 버스와 스포츠카


Q. 서버가상화
 hp superdome cellboard . 셀보드 2개와 IO박스 한개로 서버 하나로 운영. 추후 셀보드를 3개 IO박스 한개로 서버 운영 할수 있음.



supervisor : 장비의 관리하는사람?
hiypervior : 슈퍼바이저와 구분이 필요해져서 나오기 시작

os 가 가상화 소프트웨어와 합쳐져 있으면 type1
os 가 가상화 소프트웨어와 합쳐져 있지 않으면 type2 (window에 vmware 설치해서 쓰는거)

guest os : vm 에서 올라가는 os


VM에서 해당 코드를 실행한다면
```
a = a + 1
printf("Hello World");


LD $a, r3
ADD r3, #1
ST r3, $a
```

인스트럭션이 호스트 CPU로 한번에 가지 않음. 
1. 호스트 PC 의 CPU 와 게스트 PC의 CPU 가같지 않을수 있음.
2. 어드레스 스펙이 다름

amdv, intel vtx : cmos 에서 켜고 끄고 할수 있음. 가상화된 인스트럭션을 호스트 PC에서 바로 사용할수 있음.


para virtualization
반가상화


게스트OS 가 하이퍼콜을 함


## isolation이 주는 장점
### infra 관리측면
장애격리
관리분리
on/off 별도 진행
### OS격리
OS 문제 발생시 격리
### app 격리
개발 측면 유리


```
hostname <- OS
IP
FileSystem
process
user
ipc
```


유닉스의 게스트계정 방식
```
chroot /home/guest          // 루트를 변경 시켜서 여기서 못 벗어나게함. 다른곳 접근 차단해서 시스템 보호
choroot jail 이라고 부름
```

jail 이라는 용어가 안좋아서 container 았다. 어쨋든 정해진 구역에서 보여지는 환경. 도커에서 용어를 만들어서 컨테이너라는 용어로 쓰임. 프로세스의 격리된 환경

LXC 에서 기술이 발생하였지만 AppContainer Containerd가 쓰임
lxc -> labcontainer -> oci -> containerd

컨테이너별 네임스페이스 격리, cgroup 으로 그룹으로 구분하며, 시분할시켜 자원을 사용/배분하여 관리함
커널 3.08 부터 쓸만해짐.


https://en.wikipedia.org/wiki/Linux_namespaces
https://en.wikipedia.org/wiki/Cgroups

차등화된 스케쥴링 기능이 필요해져서 control 가능하게 만듦

도커의핵심기술은
`컨테이너가 사용하는 파일시스템환경을 다른 컨테이너로 실행 시킬수 있게함`


- 일반적인 개발은 install 파일을 만들어서 설치하라고 전달함. 설치가 안되면, 왜그러지? 환경에 구애받음
- 도커파일 만들어서 운영 환경에서 배포. 환경에 구애받지않음

소프트웨어 배포에 최적화된 플랫폼
