# Newtwork Basic (7/29~8/1)
``` 
* Network : 정보 교환을 위해 통신 장치를 연결한 통신망
1. LAN (Local Area Network) : 근거리 고속 통신망
2. WAN (Wide Area Network) : 원거리 (광대역) 안정적 통신

* Internet : 전 세계적 통신망의 집합
* Protocol : 네트워크 통신을 위한 규칙 (문법 + 의미 + 순서)
* Network Model : 호환을 위한 통신망 제작 모델 / 문제 해결

* 부호 : 의미를 가지는 약속된 기호
* 신호 (Signal) : 부호가 특정 매개체를 이용해 전달되는 상태
 - 전기 에너지, 통신망 필요

* OSI 7 계층 : ISO에서 지정한 네트워크 모델 (물리적 하위 계층 + 데이터 활용 상위 계층)
* TCP/IP : OSI 7 계층을 4계층으로 재구성           
```
    
<br>

7 OSI 계층
----------
|7 OSI 모델|TCP/IP|역할|
|-|-|-|
|애플리케이션 + 프레젠테이션 + 세션 계층|애플리케이션 계층|APP 작업|
|전송 계층 |전송 계층|송신, 수진지의 데이터 신뢰성 확보|
|네트워크 계층|인터넷 계층|경로 탐색|
|데이터 링크 계층|Network Interface 계층|장치 간 데이터 전송 방식|
|물리 계층|Network Interface 계층|장치 연결, 신호 전달|

<br>

**1. OSI 물리 계층 : 신호 전달을 위한 물리적 연결**
 * 케이블 : 장치, 네트워크를 연결하는 물리적 매체로 데이터를 전송하는 전선 <br>
   -LAN Cable : UTP, FTP, STP
 * 리피터 : 신호 증폭, 재생
 * 허브 : 네트워크 장치를 연결하여 데이터 중계, 전송 -> 스위치로 대체

<br>

**2. OSI 데이터 링크 계층 : 장치간 운송방식 지정 -> 신뢰성**
 * L2 Switch <- 초기 이더넷 CSMA/CD의 충돌
 * 장치 식별 + 오류 제어 + 흐름 제어
 * LAN : Ethernet
 * WAN : HDLC, Frame-relay, PPP, ATM

<br>

**3. OSI 네트워크 계층 : 경로 탐색**
 * Router
 * IP : 기본 주소 (IPv4, Ipv6)
 * ICMP (Internet Control Message Protocol) : 통신 가능 여부 판단 (ex Ping)
 * ARP (Address Resolution Protocol) : MAC 주소와 IP 주소 연결
 * Routing Protocol : 최적 경로 탐색

 <br>
 
IPv4
----
* IPv4 통신방식 : Unicast, Broadcast, Multicast <br>
* 서브넷 마스크 : IP 지정 <br>
* 클래스풀 : IP를 규격화된 클래스로 구분하는 방식 = 10.12.31.0 / 24 -> 255.255.255.0 <br>
* 클래스리스 : 클래스 구분 없이 IP범위를 가변적으로 구현 = 10.21.31.0 / 8 -> 255.0.0.0
  1. A클래스 : 8비트 = 255.0.0.0   
  2. B클래스 : 16비트 = 255.255.0.0   
  3. C클래스 : 24비트 = 255.255.255.0  
```
IP 주소 표현
IP : 10.5.4.9
서브넷 마스크 : 255.0.0.0
네트워크 IP : 10.0.0.0
사용 호스트 IP : 10.5.4.9
호스트 범위 : 10.0.0.1 ~ 10.255.255.254

서브넷 마스크 : 255.255.0.0
네트워크 IP : 10.5.0.0
사용 호스트 IP : 10.5.4.9
호스트 범위 : 10.5.0.1 ~ 10.5.255.255

서브넷 마스크 : 255.255.255.0
네트워크 IP : 10.5.4.0
사용 호스트 IP : 10.5.4.9
호스트 범위 : 10.5.4.1 ~ 10.5.4.254
```
 <br>
 
### Cisco 실습
1. 지정 IP 입력
2. PC, Router에 맞는 IP, 서브넷 마스크 입력
3. ICMP로 실행 확인 (+ARP)

![353716662-dc55db80-cfc0-4086-b747-3477cf621ac8](https://github.com/user-attachments/assets/af429c20-9678-4879-be9c-b34a82547fe9)

 <br>
 
**Routing Protocol : 경로 탐색 (Router 간의 통신)**
* 정적 : 관리자가 직접 경로 설정 <br>
  -Static : 설정한 진행 방향 (목표 PC의 노드 / 서브넷 마스크 / 진입 라우터 IP) <br>
  -Defualt : 모든 진행 방향 = 진행 방향이 하나인 말단 라우터 (0.0.0.0 / 0.0.0.0 / 진입 라우터 IP) <br>

 ![static](https://github.com/user-attachments/assets/68447ee1-a21e-4e0e-828d-a919dec4f3fc)
 
* 동적 : 전체 경로 학습 -> 자동 최적 경로 계산 (네트워크 변화에 민감) <br>
 -AS (Autonomous System) : 자치 시스템 = 관리자가 관리하는 라우터의 집합
   1. EGP (Exterior Gateway Protocol) -> BGP
   2. IGP (Interior Gateway Protocol)
      -Link-State : 수렴 시간 빠름, EIGRP OSPF                  
      -RIP : Distance Vector - Hop이 가장 적은 경로 (라우터에 연결 노드 모두 입력)
 
![rip](https://github.com/user-attachments/assets/f9522f45-c0eb-4861-be16-697edbb53a98)

 <br>
 
**Sever**
* DNS (Domain Name Service) : 문자 주소 + IP (숫자 주소) = www.naver.com + 223.130.200.236
* Web Service : 하이퍼텍스트 형식의 문서파일 제공 (Hyper Text Markup Language, Hyper Text Transfer Protocol)
 1. DNS server의 Services DNS에 웹사이트 문자 주소와 IP 추가 (IP칸 DNS Server 미입력)
 2. Web Server에 IP 입력 (IP 칸 DNS Server 미입력)
 3. PC IP칸에 IP 입력 (IP 칸 DNS Server 입력)
 4. PC Web Browser 칸에 서버 주소 (문자, 숫자) 입력 시에 연결 가능 여부 확인
    
![dns](https://github.com/user-attachments/assets/6f60bda0-5e5e-4aaa-af48-eae48c20bb4e)


출처 : [윤서짱 로깅](https://github.com/100chun/Coding_Log)
