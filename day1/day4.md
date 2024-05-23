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

