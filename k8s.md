1. 기본 개요
  1. 인프라 구축 및 쿠버네티스 이해 - 환경(Dell 미니형 PC X 2, GPU없는 데스크탑 X 3) linux 24.04 
     - Control plane(데스크탑 1)
     - Worker node(데스크탑2,3, 미니피시 1)
     - 임시(미니 피시)
  
       쿠버네티스란 : <img width="875" height="256" alt="image" src="https://github.com/user-attachments/assets/9b4fec26-d002-456e-af67-d283a1274cbf" />
        솔직히 정의로 이해하기 어려워서 내 말로 이해하면 -> 그냥 컴퓨터 여러대를 한대에서 관리하는거.
        장점 : 서비스 디스커버리와 로드 밸런싱, 스토리지 오케스트레이션, 자동화된 롤아웃과 롤백, 자동화된 빈 패킹, 자동화된 셀프힐링, 시크릿과 구성 관리, 배치 실행, 수평확장, 확장성을 고려한 설계
        -> 서버가 여러개 떠 있어도 컨테이너가 알아서 트래픽 나눔
        -> 디스크 연결 자동으로 지가 함
        -> 배포하다 망하면 이전 버전으로 돌림
        -> 서버 자원 알뜰하게 씀
        -> 죽으면 알아서 다시 살림
        -> 비밀번호 토큰 같은걸 코드로 안쓰고 지가 어따가 잘 놨둠
        -> 일회성 작업 같은것도 서버 관리 없이 실행함
        -> CPU 사용 많아지면 POD를 알아서 증가시키고, 적어지면 다시 없앰
        -> 코드 안바꾸고 인프라만 키울수 있음, 컴터 늘리면 그대로 확장됨
  그리고 역사에 대해 막 써 있던데 굳이 알 필요는 없으니 넘어감
  
  2. 쿠버네티스 컴포넌트
     컨트롤 컴포넌트 control component
     - kube-apiserver(API), etcd, kube-scehdueler, kube-controller-manager, cloud-controller-manager
     노드 컴포넌트 node component
     - kubectl, kube-proxy, CRI(container runtime interface)
     애드온( 이부분 아직 잘 모름)
     - DNS, 웹 UI, 컨테이너 리소스 모니터링, 클러스터 레벨 로깅
    - 뭐가 너무 많으니 실습하면서 정리
  
      
  3. 클러스터 관리 도구
    kudeadm, kops, kubespray
    이것도 나중에 실습하면서 정리

2. 노드
   <img width="889" height="321" alt="image" src="https://github.com/user-attachments/assets/764afc68-d1d9-4658-8ab4-315ab3c95c3d" />
   컨테이너(container) : 도커의 컨테이너 개념과 유사(컴퓨터가 작업하기 위한 환경)
   파드(POD) : 컨테이너 집합
   워크로드 : 클러스터의 컨테이너를 동작시키고 관리하기 위해 사용하는 오브젝트
   컨트롤 플레인 : 컨테이너의 라이프사이클을 정의, 배포, 관리하기 위한 API와 인터페이스들을 노출하는 컨테이너 오케스트레이션(총괄하는 도구)

   -> 일단 대충 작업관리자라 이해하면 될듯
   
   API 서버에서 노드 추가하는 방법
    문서 참고 https://kubernetes.io/ko/docs/concepts/architecture/nodes/
   

4.실습 연습한거 위주로 정리
  4.1 kubectl 설치 
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
  4.2 kubectl convert plugin
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl-convert"
    sudo install -o root -g root -m 0755 kubectl-convert /usr/local/bin/kubectl-convert
    4.1 4.2부분은 버전문제 발생할 수 있으니 공식문서에서 매번 참고해야함 
    
  4.3 swap off (스왑 메모리란 실제 메모리 ram이 가득 찼지만 더 많은 메모리가 필요할때 디스크 공간을 이용하여 부족한 메모리를 대체할 수 있는 공간)
      데스크를 메모리처럼 쓰면 스케줄링 판단이 꼬인다는거 같음
    sudo swapoff -a
    /etc/fstab 이 파일에서 # 이 줄을 주석처리 해준다.# /dev/mapper/centos-swap swap swap defaults 0 0
  4.4 CRI는 대표 3개있는데 
    containerd, CRI-O, Docker 
    그 중 containerd 사용(이유 : 그냥 하라고 해서)
    sudo apt-get update
    sudo apt-get install -y containerd

    
  4.5 kubeadm 설치
    sudo apt-get update
    sudo apt-get install -y kubelet kubeadm kubectl
  여기까진 모든 컴퓨터에 설치필요
5. 실행 
  5.1 Control plane 초기화
    sudo kubeadm init 
    이거 하면 마지막 줄쯤에 kubeadm join ... 하고 뭐 뜨는데 그걸 노드로 사용하고 싶은 컴에 입력해주면 됨
    plaine 노드에선 
    mkdir ... 라고 3줄짜리 명령어가 있는데 그거 그대로 입력
  5.2 CNI 설치(container network interface) 이거 없으면 노드끼리 통신 안됨
    너무 많은 cni가 있어서 상황마다 다르게 선택
    - 1.22
    
  
