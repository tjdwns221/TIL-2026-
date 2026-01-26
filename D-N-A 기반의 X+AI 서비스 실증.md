### 1 2주차 (서론 느낌)
AI, HPC, HPDA는 데이터를 활용
박스는 리누긋에 
박스 펑션 인터 코넥트를 활용해서 시스템을 만듬
베어메탈막스 전체를 갖는 펑션 (하드웨어 성능을 최적화해서 풀 성능(
컨테이너펀셩,도커는 기능 역할 중요도에 따라 환경준비
provisioning, orchestraning 
구조 
앱 론칭 -> 통신 -> 클라우드 데이터 센터
클라우드 데이터센터에선 3tier 구조로 대응 
web -> app -> DB 
HPC/HBDC에서 DB에서 처리하는데 이게 인공지능 원리
x+AI서비스를 실체화 하려면 클라우드 네이티브한 펑션을 활용하는 서비스사용하고 HPC/HPDC에서 활용

오픈소스 버전 + 자원을 오케스트레이터 스케줄러로 데브옵스가 관제탑에서 관리
ai는 결국 생태계를 통해 확산 가능하고, 그걸 하는게 우리가 하는 역할이다
digital twin 기반 살아있는 
software defined 

데이터 네트워킹 에이아이 
핵심적인 원리는 최종 서비스를 위한 인프라개선 및 도구화를 통해 단계별로 디지털 트랜스퍼밍 

###  3주차 1차시
네트워킹 기초
네트워킹이란 뜻은 연결하다, 이동하다 네트워크는 시설임
underlay physical networks(공유도로) 
networking top down approach 도서 추천

Access networks : 가정에서 연결
 core networks : 중앙에서 연결 – 많이들 알고있지만 구조적으로 알고있지 않아서 언급
일반적으로 사람들은 네트워크의 끝단만 알고있음(와이파이, 랜선사용)
구조적으로 알아야 구축 연결을 할 수 있음
앤터프라이즈 넷트워크 – 네트워크는 시스템이다(굉장히 방대함)
[사진1]
도로에서 규칙이 있는거처럼 네트워크에도 규칙존재
OSI 7계층
[사진2]

논리적으로 7계층이지만 현실세계에선 5계층으로 단순화함

네트워크에서 문제되는 상황을 loss, delay, throghput 이라고 하고, 이것들이 상호작용함
QOS triangle은 위의 3가지를 구성하는 삼각형인데 이 3개를 모두 만족시킬수 없음(상충관계)
delay 감소하면 throughput, loss가 증가, loss가 증가하면 throghput 감소
프로토콜, latency 개념이 다르게 나오지만 결국 이거 같음

해킹에 대응하기 위해 cyber security도 고려하며 네트워킹을 해야된다
###  3주차 2
네트워크 레이어
ip tcp는 네트워크 레이어에서 나옴
virtual cirkit 
router datagram의 경로를 안내함(routing)
router는 datagram 검사 -> 목적지 확인 -> 경로제시
라우터 내부엔 스위칭이란 기술이 적용됨 (이게 어디로 보내는지 알려줌)
스위치는 내부경로 라우터는 대기
head of line blocking 앞이 막혀서 길이 막힌 상황
router의 역할 올바른 경로 안내, 데이터를 잘 분배해서 처리, 최적경로 제시, 빠르게 처리

트랜스포트 레이어, 인터넷 프로토콜에선 어느주소에서 왔고, 어느주소로 가려는지 알수있음(sourch ip address, destination ip address, packet size) 
ipv4 에선 fragment이슈 존재( maximum transport unit-1500bite로 자름)
[사진3]

스위치에서 꽂으면 다른곳으로 연결되는걸 스위치가 함
그리고 스위치는 어디로 연결하는지 알려주는걸 DHCP라함 
NAT(network address translation)
ip 주소의 원칙 전세계에서 physical ip address가 존재해야하는데 ipv4가 부족함 그래서 한 개의 주소를 여러개로 나누어 분배함 이걸 당담하는 역할이 NAT임
이 방식은 가정 회사 어디서든 활용함
- 1대다 구조임
이 구조 때문에 전세계에 인터넷이 연결되는것임
ICMP(internet control message protocol) 데이터 전송실패 원인을 메시지를 통해 알려줌
근본적으로 주소가 부족한 ipv4 때문에 ipv6을 사용해야하지만 변경하는게 복잡해서 현재 혼재된 상태

라우팅을 이해하기 위해선 그래프를 이해해야함
node, link, path 
라우팅을 정리해주는 알고리즘은 global : Link-state(LS) algorithms Distance-Vector Algorithms 두가지 알고리즘이 다양하게 복잡하게 존재

계층적 알고리즘(hierachical routing)-7계층
여기서 어떤 계층에서 누가 다룰것인가라는 문제 존재
ASs(autonomous Systems) 나라별 주소 부여(나라별 economical이란 단어 혼재해서 사용)
intra-AS는 하나의 AS 내 라우터 간의 관계
inter-AS는 AS와 AS간의 관계, Border gateway protocal(BGP) 사용-어디를 어떻게 갈지 고민
ASs router가 잘못된 정보를 뿌리면 인터넷에 혼란이 발생
[사진4]

broadcast routing은 전체범위, multicast routing은 제한적 범위에서 하는방법(자막이 좀 이상함)
### 3주차 3차시
transport layer
path를 통한 데이터 전송 및 확인
 internat의 성공이유 IP를 통일했기 때문 (IP만 통일하면 TCP, UDP 등 응용가능) - 모래시계구조
End-to-End principle
End: 모든일 처리, core:길 안내 역할, internet 초기 : router의 기능 및 장비들의 데이터 처리 능력 미흡
dumb core(pipes)+ smart end라는 원리로 만들어진게 ene to end principle이고 이게 ip임

internet선 + UTP케이블 = ethernet 방식으로 link가 잡힘, 이것들이 ip를 가짐

ip는 길을 안내, TCP,UDP는 어떤 물건이 가는지 알려주는 역할
link는 도로고 ip는 차선, TCP/UDP는 물건

컴퓨터 안에 data(Socket)이 들어오면 내부적으로 어디다가 전달해야 할지 정해야함 
Process안에 포트를 통해 전달 – 컴퓨터 안에 네트워크가 또 이루어져 있다

TCP 믿을만한, 전달여부 확인, UDP 빠르게 전송, 나중에 전달 여부확인
현재의 인터넷은 TCP를 근거로 internet 서비스를 생성
transport layer는 경로 방식을 고려하여 최종목적지(application)에 전달 Socket-port-process

UDP header = Data의 port number, 주소, 크기를 하나씩 끊어서 따로따로 전송, 그리고 나중에 check usm을 보내서 확인함 만약 첵셤에서 확인해보니 이상하면 다시보냄 
데이터 수신 확인 : ACK 잘 받았어, NAK 못 받았어, DUplicate ACKs 데이터 받았는데 순서가 이상하게 받았어
잘 받았는지 확인 정리 : checksum, timer, sequence number, ACK, NAK, window/pipelining 
마지막 윈도우 파이프라인은 전체 다 보내고 확인(이러한 6가지 방법을 통해 확인함)

TCP에선 Three way handshaking구조 잘 받았는지 확인
transport reliability 확인시 유의사항 : 시간 효율성 고려, 상대편에서 확인가능한 적정량 보내기
전송량 관리, 전송속도 관리를 flow control이라 함
[사진5]

Congestion control : 길이 막힐 때 어떻게 보내야할지 고민하는 것 이걸 고려하여 적당히 고려함
slow start, congestion avoidence, fast recovery, fast retransmit 등 세부 원리 존재
중요한건 길의 사정을 보면서 보내는 방법을 고민한 것
TCP Reno : AIMD(adaptive increas muliplicative decrease) – 가장 주된 세력중 하나
길을 계속 확인하면서 조금식 늘리던가 아님 다시 줄이던가 하는 것
길을 여러개 있을 경우 fairness & parallel/Multi-path TCPs
High-speed TCP 빠르게 보내는 방법

WEB: 빠른 데이터 처리에 특화된 방식(TCP와의 비교는 안정적 but 느림 http 방식은 TCP방식임) 
QUIC(quick udp internet connections)는 속도가 빠른데 여긴 빠름(이부분 자막 이상함, 마지막쯤)
강의이외 내용으로 찾아보니 http3.0부터 적용되고 TCP장점과 UDP 장점을 합치려고 만든구조 UDP인 이유는 껍데기를 UDP를 사용했기 때문 

### 4주차 1차시 Application 계층의 기본 개념과 역할 이해, 그리고 대표적인 protocol의 원리와 동작 방식
,CDN(content distribution network)와 p2p 네트워크 동작원리 분석

어플리케이션에선 TCP, socket, 
연결과정 network -> computer -> socket -> port -> application
교수님 : (socket programing 방법 공부 추천
[사진6]

[대표적인 어플리케이션] 

WEB : HTTP(hyper text transfer protocol) 읽을수 있게 설계됨 – IP > TCP > application
웹서버 : 정보를 전달하는 메인서버, 캐시서버 : 가까운곳에 저장된 서버
Web이 느린 이유 1. TCP 기반 2. WEB안에 다양한 material들 존재하고 다양한 source에서 오기 때문에 이를 개선하기 위해 Transport protocol quic 사용 

FTP(file transport protocol) : 예전에 존재했던거
in band va out of band ?? 이러하고 그러하다? 무슨 말이지
control and data connections
Simple mail transfer protocol 
RFC(request for commnets) IETF에서 쩨공하는 다양한  protocol 규칙을 통일해서 정의한 문서, 번호부여 일관된 근거
데이터가 적절한 어플리케이션에 들어가는 방법
DNS
IP Address 할당자 -> Domain name service 제공 및 전달
[사진7]

DNS도 hierachy를 가지고 있음 DNS도 계층으로 지어져 있음 bind는 IP와 DNS를 묶는다는 개념으로 이해
DNS Attack Surface vs DNS Security : 굉장히 중요함
P2P(Peer to Peer) : Bit torrent가 예시임
공급자가 메인 서버가 아닌 일반 사용자가 서버가 될수있음 초기 internet speed가 느릴 때 copy를 주고받는 개념 유선 network 및 모바일 상황에서도 활용
P2P에서 단점은 누가 어떤걸 가지고 있다는걸 모른다는 




거임 
Distributed hash table 해쉬는 데이터를 요약하여 단순화하는 것 hash function은 데이터를 넣으면 해쉬값을 줌 그건 거의 항상 고유의 값을 가짐 해쉬를 중심으로 데이터 구분 
DHT 상대편의 주소와 정보 확인 정도로만 설명하시고 넘어감 
### 4주차 2차시 
link 계층의 역할과 주요 프로토콜을 이해, error detection 및 correction 메커니즘, LAN(Local Area Network)의 구조와 MAC 주소 VLAN의 원리를 분석

Link 연결하는 것 이 계층은 다음 목적지를 가게하는 방법(물리적인 측면에 가까움)
링크계층의 대표는 Ehternet
link는 error detection, correction 두가지를 다룸
Error detection 1. parity check 2. checksum 3. crc 
forward error correction code : 데이터보다 더 많은 bit를 보냄 그래서 몇 개가 깨져도 복원이 가능함 (encoder –decoder 구조)

MAC(multiple access protocols)에서 정하는 것 :Channel partitiong protocol, random access protocol, taking-turns protocols을 다루여야 함(그래서 multipel임)

MAC:Channel partitioning protocols : 
FDM(Frequency division multiplexing), TDM(Time Division Mulitplexing), CDMA(CodeDivision multiple access – 어떻게 가야 충돌이 안날것인가에 대한 프로토콜
ALOHA, slotted aloha, CSMA/CD(Carrier Sence Mulitple Access/Collision Detection) : Carrier가 전기적인 신호를 보내기 때문에 sensing 이됨 충돌이 난 경우 전송을 취소하고 기다림 기다릴 때 랜덤하게 들어감
Polling protocol, token-passing protocol 결국 이 다양한 프로토콜은 하나의 링크에 어떻게 잘 믹스해서 보내는 방식이라는 것


케이블 모뎀을 쓰는 DSL방식, 케이블 TV+Internet +network , 광 internet을 직접 network선을 넣는 방식 3가지가 존재함

LAN(Local area Networks) : LAN내부에 기본체계, 주소 존재
link Layer개념의 주소가 중요함 LAN에 들어가려면 MAC+IP 둘다 있어야함 IP는 가상주소고 MAC은 하드웨어 주소임 
ARP(Address Resolution protocol) MAC과 IP

가상 LAN(VLAN) : privacy가 필요할 때 사용하는 기능 
SWitch들이 VLAN ID와 트래픽이 섞이지 않도록 Isolation함 
MPLS(MUltiprotocol lobal Switching) : ATM(Asynchronous Transfer Mode)기반의 Circuit Switching 방식으로 개발된 방법 IP 쪽으로 변형되서 사용하고 있음 core network에서 핵심적으로 빠르게 처리하는 기법 Special한 link를 찾는방법

시나리오 : 데이터센터안에서 데이터가 어떻게 움직이는가 > 밖에서 request가 들어오면 안에서는 20배의 트래픽이 발생 따라서 체계적 확장적으로 만들어야함
[사진8]

Web APP DB가 젤 중요함(3-tier Application server)
웹서버 -> 어플리케이션 서버 -> 디비서버 패턴이 대부분 인터넷 패턴임
[사진9]

### 4주차 3차시
네트워크 보안의 핵심개념을 이해하고, 주요 암호화 및 인즌기법의 원리, firewall,IDS, IPS,Zero Trust Security등 보안 메커니즘 분석

네트워크 보안이란 ? comfidentiality, message integrity, end-point authentication, operational security 이 4가지
cryptography 암호화 하는 기법, 점점 더 길고 복잡하게
Symmetric : 잠그는 key와 여는 key가 동일해야한다
Asymmetric : 비대칭키 

Public key Encryption : 잠그는 key와 여는 key가 다르다? 공개한 publickey를 private key로 풀수 있게 특정을 허용
어떤 사람이 풀려고 시도하면 private와 쌍이 맞으면 풀수 있음 – private key까지 알아야 풀 수있는것임

Cryptographic hash functions 텍스트 데이터를 hash값으로 바꾸는 것 MD5 Hash Alogrith(128-bit hash) Hash값을 보내고 맞는 해쉬값이면 풀어주는 기법
messgae integrity : Digtal signature(서명), Symmetric key Cryptography, public priavate key combination 
PKI(Public key infrastructure)(공인인증서 개념)
원래는 PKI중심에서 다양한 개방형 securty로 변환하는추세 

 Password Replay Playback, One time password(OTP) 방식도 유용하게 사용
Securing E-Mail : Digital Signatures, Securing E-mail 
Transport layer에서 SSL 생성 - TLS SSL(Securing TCP Connections) 
[사진10]
이 방식으로 작동

무선 LAN Security 다양한 Standard 확장 및 생성되어 체계적으로 관리
유선 LAN Securty 이 부분 뭔가 설명이 이상 둘 중하나는 보완이 철저해야한다라고 하는데 상식적으론 무선 LAN이 더 중요할거 같은데 설명에선 유선이 더 중요하다고 나옴(찾아보기)

Firewall : 트래픽을 검문하고 차단하는 것(성문같은 개념, APllication Gateway) 다양한 레벨로 확장되어 존재 
zero trust Security : 보완의 핵심원리 나말고 아무도 믿지마라 공격수단은 너무 다양하고 방대함
IDS(Intrusion Detection Systems) : 공격 탐지 및 대응
IPS() : 공격예방

Honey pot : 공격 유인 후 방어
DMZ(Demilitarized Zone): 1차 방어선 개념
IP Table : 각 머신에서 방문을 걸어 잠그는 개념(port 막는건가?) ->  이게 성능이 좀 떨어져서 eBPF(Berkeley Packet Filter)로 IP table을 개선

### 5주차 1차시 
Software-Defined Networking(SDN)의 기초개념과 도입배경 이해, 기존 인터넷의 한계와 SDN의 필요성, 미래 네트워크 핵심 기술 트랜드

hyper connected software defined 이 두가지가 젤 중요함

Network 확장 -> 복잡하고 보완중요 -> refresh node -> network 역할론

XIA 단말기 고유 주소 부여를 위해 IPv6로의 전환 논의
MF(Mobility first)
NON(named DATA Networking)S DN과 같은 계열: 미래 인터넷 아키텍처 후보들

Software-Defined Networking & OpenFlow
네트워크의 제어 기능(Control Plane)과 데이터 전달 기능(Data Plane)을 분리하여
네트워크를 소프트웨어로 중앙 제어하는 구조

Flow: Network에서 data가 흐르는 것 Link들이 있는 PAth에 Flow가 넘어갈 때
link 들이 있는 Paht에 Flow가 넘어갈 때 Controller가 flow를 일일이 control 하면서 가이드하는 방식 

control평명과 data 평면이 연결되면서 조화롭게 일할 수 있는 환경으로 바뀜
software-Defiend 개념이 적용가능한 신형 또는 기존 장비 보완작업

Control flow조정과정 Tag(패킷에 라벨 붙이기) -> Steer(경로 유도) -> map(서비스 매핑)
대표적인게 onus, opendaylightt,apic 이렇게 있음


P4는 네트워크 장비를 프로그래밍하는 언어 - openflow는 아직은 좀 남아있었다면 P4는 아예 언어적임

Overall Infra Sector를 End,Edge,core에 연결한 상태에서 서비스 제공 = 이 말이 전체에 SDN을 적용한거라 함
이걸 SDI(Software-Defined Infra)라 말함
Digitla SOC에 SDI가 적용 되어야함
디지털 SOC(Social Overhead Capital)는
도로, 철도, 하천 등 기존 사회기반시설에 AI, IoT, 5G 등 디지털 기술을 접목하여 안전하고 효율적으로 관리하는 지능형 인프라

-- 여기까지가 SDN,SDI 내용이고, 이건 어찌보면 변화임, 이후 근데 기존 방식에 조금 발전시킨방식 설명
[이쯤에서 한번 정리]기존 네트워크 문제 장비가 스스로 판단 (복잡), 중앙 제어 불가능, 자동화 불가
 SDN 해결 : Control/Data 분리, 중앙 Controller, Flow 기반 제어, OpenFlow, P4로 네트워크 프로그래밍
미래 :Hyper-connected, SDN + NFV + AI ,콘텐츠 중심 네트워크(NDN)
EVoluitino path Swith,routing의 구분이 없어지고 layer가 확장됨
Tunneling packet을 터널을 만들고 감싸서 전송
VXLAN(구분 확장 및 Label을 붙여 터널을 만듬) 
Overlay 터널들을 이용해서 Overlay Networking을 완성하여 사용함
[사진11]

### 5주차 2차시
SDI(Software-defined infrasturcture)와 SDN의 정의를 이해하고 연관성,SDN을 중심으로 하는 현대 네트워크 구조의 주요요소를 학습, SDN이 네트워크 가상화 및 보안에서 제공하는 이점을 파악한다.

NFV(Network Functions Virtualization) 가상화 NFA 이건모든 영역을 건듬
[사진12]

SDN에서 가장 핵심은 네트워크 장비의 Control Plane(제어부)와 Data Plane(전송부)의 분리(SDN(Software Defiend Networking) : 네트어크 장비의 controlPlanem(두뇌)를 중앙 소프트웨어로 빼버림
전통 네트워크는 스위치가 제어 전달 다 했는데, SDN에선 컨트롤러가 제어하고, 스위치가 패킷전달만 함

Cloud-native Application Friendly한 Networking 형성 -> SDN과 NFV 기술이 합쳐져 Overall Infra Sector에 담김

SDI = 모든 인프라를 소프트웨어로 정의하는 세계관
SDN=네트워크 담당, NFV= 네트워크 기능을 VM/컨테이너로 만든느 기술 이 둘이 합쳐져서 Cloud-native 통신 인프라가 됨

Slice = 전용차선, Slicing Arrays 기술 구현 = Slices의 요구조건 만족, 차별화 및 효율적 지원 방법 생성 
Slicing 6G 진행형, 5G NSA(Non-Standable),SA(Standablone)[독립적으로 실행될수 있는 소프트웨어]
Network Slicing - 하나의 물리 네트워크를 여러 개의 논리적 네트워크로 쪼갬

Slicing 적용 영역 : Open RAN, OpenRadio Access Network, Private Network
| 구분  | 의미                    |
| --- | --------------------- |
| NSA | 4G 코어에 5G 무선만 붙인 임시버전 |
| SA  | 코어까지 전부 5G (진짜 5G)    |


RAN (Radio Access Network)

기지국 쪽 네트워크 (휴대폰 ↔ 기지국)
예전:
삼성/화웨이 장비 = 폐쇄형 블랙박스


Open RAN:
기지국도 SDN/NFV처럼 모듈화 + API 공개

구성:
RU: Radio Unit
DU: Distributed Unit
CU: Central Unit

→ 각각 다 컨테이너/VM으로 분리 가능


 엣지 컴퓨팅(Edge Computing)은
데이터가 생성되는 지점(엣지)과 가까운 곳에서 데이터를 즉시 처리하는 분산 컴퓨팅 방식으로, 데이터를 중앙 클라우드로 모두 보내지 않고 로컬에서 분석해 응답 속도를 높이고 네트워크 부담을 줄이는 기술
원리 : smart 장비들의 유기적 연결 -> Service 제공 뒷단: Cloud base 트레이닝 모델생성 앞단 : 추론을 통한 적용 및 검토
스마트 팩토리도 같은 원리임 

open source level에서 edge computing 과 radio access network 기술을 연결

*fabric* 끝단에서 core 쪽으로 갈수록 촘촘하게 연결되는것처럼 보이는데 이걸 fabric이라 표현함
외부말고도 내부에서도 fabric이란 용어를 쓰는데 ai장비들을 빠르게 연결하는 interconnect

좀 다른 얘기긴 한데 : 
Cloud 기반 computing resources와 저장소 연결할때 데이터 검증시 blockchain으로 서비스에 대한 신뢰 부여
이걸 ABCD라 하는데 AI,Block chain,Cloud,Data를 연결한다 함


거점도시연결에서 쓰인 fabric은 데이터센터에서도 사용되고 여기선 데이터 연결성이 확보된다는 뜻으로 이해
*fat-tree*가 페브릭 콘셉안에서 유기적 입체적 성격을 나타냄

### 5주차 3차시 - HPC와 AI의 융합 및 이를 지원하는 네트워크 구조, Hyper-connected Networking이 HPC-AI환경에서 제공하는 역할, X+AI서비스의 구성과 Hyper-connected Networking

Digital SOC(Social Overhead Capital) : Computer Systems Everwhere
효율적 infra build를 위해 
공유형으로 구현, 플랫폼 운영 방법 차별화 불필요

| 공유infra | 공통 platform |
| ------ | ------------| 
| 같이쓰는 infra | 같은 rule base 활용 |
| 규칙적 운영 | |
| 자동화 | |

-> DevOps  = 개발자와 운영자가 공유함
문제는 같이 쓰다보니 보안문제를 해결해야함
-> DevSecOps 
AI + HPC + HPDA를 합친 인프라를 자동화를 위해선 cloud,cluster 기법을 활용해 규모를 키워야함 
-> Hyper connected -> 미래형 네트워크가 해결가능함


zero copy data transport = 데이터를 전송할때 cp없이 하는것 RDMA(remote direct memory access)라고도 부르고 data transport 효율성 증가함

container에 function을 설치한 후 연결해서 활용 MSA(micro service architecture)기반, service chining or service composition
이것의 핵심수단이 hyper connetecdd

 #### 정리
 미래 네트워크는 Hyper-connected와 Software-defined를 핵심으로 하며, SDN은 네트워크의 제어부와 전송부를 분리하여 중앙 제어와 자동화를 가능하게 한다. NFV는 네트워크 기능을 가상화하여 소프트웨어 기반으로 제공하며, SDI는 네트워크, 서버, 스토리지를 포함한 전체 인프라를 소프트웨어로 정의하는 개념이다. 이러한 기술은 Overlay Networking, VXLAN, Network Slicing과 결합되어 5G/6G 기반 Cloud-native 통신 인프라를 구성한다. Open RAN과 Edge Computing은 기지국과 서비스 처리 구조를 개방·분산화하며, Hyper-connected Networking은 AI, HPC, Cloud를 초고속으로 연결하는 미래 네트워크의 핵심 기반


### 6주차 1차 
#### 디지털 데이터의 정의와 생성과정 이해, 데이터 엔지니어링의 주요단계와 역할

DataLake, Connetecd -> Connected DataLake - 이번차시 핵심

1. Data란?, Data Storage?
   여기서 언급하는 data는 digital data

   ### digital data
   데이터 변환 과정 1. Pyhsical system 2. Transducer Sensor 3. Signal conditioning 4. Analog-Digital converter 5. computer
   여기서 temporal한 데이터 양 조절 및 양자화로 얼마나 데이터를 촘촘히 볼지 정함

Dark data : 만들어졌다가 사라지는것, 더 majority

데이터가 중요한 이유는 정보가 담겨있고 이 정보를 해석하면 지식이 되고 지식을 학습하면 지능 지능이 모이면 현명해지기 때문

데이터를 다루려면 라벨링을 해야함 - 자동화하려고 하지만 현재 인간이 직접 라벨링함

hadoop : 데이터 양이 매우 커지면서 사용 - 텍스트 중심의 데이터 저렴하게 파일 시스템을 만들고 map reduce 원리를 통해 원하는 데이터 탐색

data는 sql, no sql, semi sql 형식임

data wraehose는 structured data 중심

data lake는 raw data 중심

data lakehose raw data중심 structured와 unstructued의 조화, 디지털 데이터 approach의 major flow

## multi-modal
image, video 등 다양한 모델을 다룸

Special computing이 multimodal 중 하나?
data gravity = 데이터는 너무 많아서 옮기기 어려움 그래서 데이터가 한곳으로 모이는 특성이 존재 이를 스노우볼이라고 표현

5V Volume, variety, velocity, veracity, value 다가지 측면으로 데이터를 바라볼수 있음
-> 데이터는 포괄적인 용어


데이터를 엮어서 사용하는것을 fusion - 데이터를 융합
sensing 데이터를 흭득하는 기술, 효율적 비용절감, 프라이버시 보장 고려, mult-modal sensing이 필요


Sensing에 dominant feature 연결 -> decision point 연결


data Engineering - 데이터를 쓸 수 있게 만든것
1. DS 2. Extract, Load & transform 3. analytic Data Store(ADS) 4. Visualization & Reportion

modeling simulation = 한정적 의미의 data science

### 6주차 2차시
data storage 방식 이해

| memory | storage |
| 한시적 | 장기적 |
| 속도 빠름 | 속도 느림 |

Access 방법
file storage block storage object storage 

###### Block stoage
+ 데이터를 덩어리 형태로 가져가서 분석
+ 디스크를 블록 단위로 직접 접근
+ OS 입장에서: 그냥 디스크
+ 빠름
+ DB, VM에 사용
###### file storage 
+ 파일 시스템 형태
+ 디렉토리 구조
+ NAS
+ NFS, SMB
+ 개별적 저장 중심의 storage Entity
###### object storage
+ 꼬리표를 기반으로 특정요청에 따라 데이터를 가져오는 방식
+ key-value + metadata 기반
+ 위치 개념 없음
+ REST API
+ 확장성 최고
+ S3, Ceph Object, MinIO

하드디스크 장기, 플래시 단기
storage box 수십개의 storage가 있는 노드 만약 어떤거 고장나면 빼고 그대로 사용하면 됨
storage redundancy를 위해 스피드업, 안정성 지원(1~2개 stroage가 고장 나도 데이터 보존) 다양한 버전 존재

문제가 있을 때 원래 정보를 보관할 수 있는 형태로 저장됨
특징 : stroage 기능 특화 많은 양의 stroage drive를 넣을수 있음


하드디스크 : 용량 증가 추세 기존 1tb -> 30tb이상 (platter의 개수가 증가 -> 이거에 따라 용량증가)
SDD(Solid state drive) : 데이터에 바로 접근, 하드디스크는 개별 실린더를 돌아서 데이터를 찾는데 시간 소요

SSD 다양한 형태의 form factor가 있음 : 과거 U.2 U.3 현재 EOSFF 버전 
저장공간 : 형태가 modal화 됨, 용량도 키우고 저장하기 좋은 형태로 전환

여러 개의 Storage Node가 있음 
Storage의 대장 node, 담는 node들에게 저장업무 분배 hierachy 관계를 통해 strage 빌드업 

storage와 computing server 연결 
1. Network-Based Storage (NBS) - storage node간 네트워크 기반 연결, 
2. Network Attached Storage(NAS) - 파일 서버, NFS/SMB ,그냥 네트워크 파일 공유
3. Storage Area Network(SAN) - 블록 스토리지 전용 네트워크, Fibre Channel, iSCSI ,서버가 디스크처럼 인식

Computing box : 기본적인 저장 HDD, Flash Base SSD:빠른접속, HDD와 Flash를 Combination해서 Computing server에 활용, 계산을 위한 임시적인 저장 -> 데이터를 쌓아놓고 가져와서 쓸 때는 사용자가 조절해야함


Cloud-based Storage Sharing 
목적에 따라 Compute box, Storage box, networking box 로 구분


#### Storage medium 

punch card -> Tape base storae = 이건 여전히 대용량 데이터를 저장하긴 좋아서 아카이빙할때 사용 -> floppy disk = 이건 퇴출됨 -> USB flash memory -> SSD 중간에 side로 있는게 CD,Blu-ray등 존재함


단위의 Range 
SSD 소비자용 1TB,서버용 5~32TB 
HDD 30TB~64TB
밀도 flash가 하드디스크를 초월 
단위 면적 server에 flash를 꽉 채우면 더 큰 용량은 하는것도 가능하긴 함

U(unit) = 서버의 외향적인 크기를 나타내는 단위의 약어 U서버를 특정 크기로 랙에 배치할 수 있도록 서버의 크기를 지정, 랙에는 서버를 고정하기 위한 나사 구멍이 있고 이를 나사로 고정하여 각 서버에 필요한 공간을 쉽게 설치
랙 = 책장
U = 책 두께

1U,2U Server 
E3LS(긴 Rular)타입을 꽂는 경우 1PB 가능

하드디스크 하드 크기의 limit이 있음 발열있고, 무게도 무거움 
Tape 단점 serial Access 저장하거나 꺼낼때 시간이 많이 걸림 근데 가장 저렴함

Compuete box 의 예시 : Raspberry pi, arduino, smart phone 
Networking Box의 예시 : Switch, Router, Firewall

#### Converage SmartX boxes
Hyper-converaged box = compute, storage, network 모든 기능 존재 

여기서 한번 정리 : storage box가 모이면 storage node, 이게 또 모이면 multiple storage node 또 이게 모이면 storage server라 표현 또 이게 모이면 data warehouse라 할수 있음


#### OS 
MBA SSD, Stack으로 연결된 HDD
NVME는 SSD와 하드디스크 연결 통로의 interface, Non-Volatile Memory가 PCI Express Bus에 연결되는 방식,Storage
SCSI는 Serial line의 빠른 고속 interface, Computing System

두가지 방식 존재 : paralyze된 하드디스크 또는 flash베이스 고속 interface사용해서 데이터를 꺼냄 -> computing machine에 전달

| 방식     | 성능            | 사용          |
| ------ | ------------- | ----------- |
| Block  | Fast (Hot)    | DB, VM      |
| Object | Medium (Warm) | AI, BigData |
| File   | Slow (Cold)   | 백업          |


parallel : Ai할때 한장의 하드에 데이터 넣어놓는게 아니라 Multiple 하드디스크가 한 데이터를 협심해서 저장하고 읽는것

Parallel file system : IBM의 GPFS, Lustre 등 다양한 프로그램있음 -> 고속데이터 작업 지원 형태로 발전
특징:
+ 여러 디스크가 동시에 읽기/쓰기
+ GPU 수백 장에 데이터 공급 가능

###### Data Storage challenges
Parallel file system에서 통로가 충분히 넓어야 한다?(이거 찾아봐야할듯)


하나씩 또는 묶어서 쓰는 storage가 NBS,NAS 방식은 soft defined storage 

#### Storage connectivity
Fibre channel - Storage 연결 network, infiniBand - 고속 Network, Ethernet - 가장 일반적
다양한 physical connectivty logical connectivity속에서 storage가 연결됨


이더넷 베이스를 infiniband를 합친게 *RoCE* 라 하는게 존재 RDMA를 활성화 하는 Converged Ethernet 

운영방법에서는 HCI,SDS가 있는데  
세가지 capability(compute, storage, network)를 합쳐놓고 scale out해서 사용
Software definded storage(SDS)는 목표이고, 현실에선 HCI와 혼재함


#### 고속 특화 Access
Flash Base 재료, Parallel한것이 서포트
Optane이 이전에 뭔가 떳는데 요즘 잠잠하다? (그리고 그냥 넘어가심)
GPU안에 HBM HM 탑재 

요즘은 All flash base Storage가 대세임


#### hadoop 파일 시스템 
haddop cluster node 에 데이터를 나눠서 node한 후 탐색 -> mapreduce 방식으로 통합 및 효율화 -> 빅데이터 클러스터
(map reduce는 뭔가 빠르게 하는 방법같은데 세부적으로 모르겠네)

데이터 관리 진화 경로 
빅데이터 클러스 -> 데이터 웨어하우스 -> 데이터 레이크 -> 데이터 레이크 하우스 
= 결국 다 storage

multiple node 
node는 cpu, gpu파워를  가짐, storage cluster를 통해서 데이터를 공급, 스크래치 형식으로 parallel 상태에서 공유

node들의 gpu 메모리를 공유 테이블처럼 사용 , 메모리 테이블의 node값을 업데이트 하며 ai모델을 트레이닝함 

결론 = ai를 위해선 하드웨어가 뒷받침 해야함

추가 + Tiered Storage

Hot / Warm / Cold 자동 이동

예:

RAM → SSD → HDD → Tape

Erasure Coding

RAID의 진화판

Ceph 기본 기술

1~2개 디스크 터져도 복구

Storage Bottleneck

AI 학습 느린 이유 70%가 I/O 병목

#### 7주차 1차시 
