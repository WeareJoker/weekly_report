#Project 진행 상황

 1. 현재까지 진행된 상황
- Libtins, Dot11decrypt를 이용한 복호화 packet 분석
- parsing [kakaotalk URL, Naver Cookie, DNS] 구현, Deauth packet 구현
- 수집된 packet을 DB로 저장
- 분석 서버 구현 (http://pjhs.gilgil.net/)
- 라즈베리파이 (Kali 이미지)
- Kali에서 사용될 Bluetooth기능 추가

 2. 앞으로 '2차 평가 보고' 전까지 구현되야할 것들
  - [2-1]. 원격 조정 문제 해결 (1.AD-HOC, 2.Bluetooth, 3.ADB(Android Debug Bridge))
  - [2-2]. 기존 Plugin 테스트, 추가 Plugin 개발
  - [2-3]. 정확한 목표 방향 설정

###2번 토론 주제 내용
[2-1]. [[[3가지 주제 실습 에러 해결한 후, 이미지 캡쳐하여 올리겠습니다.]]]
- AD-HOC Network:구성하는 노드들은 자신의 물리적인 도달거리 밖에 있는 다른 노드와 통신할 수 있으며, 이는 중간 노드들이 직접 통신이 불가능한 출발지 노드와 목적지 노드 사이에 위치하여 데이터를 전달해줌으로서 가능하다.  
[http://skylit.tistory.com/180]  
- Bluetooth: [11/05 조성재 멘토님 멘토링]  
(1). Download Cross-Compiler[http://noplanlife.com/?p=1293]  
(2). Linux Kernel Source Download  ## 소스 코드 중, 라즈베리 파이 위에 들어갈 Bluetooth 기능을 가져오기 위해  
  <  in 소스 코드 >  
(3). 명령어 [ARCH = arm][.config][ARCH=arm][CC=arm-linux-gnueabi-gcc]   ##라즈베리파이 Arm형식으로 변형  
(4). 명령어 [ARCH=arm][make modules]  
(5). make menuconfig -> [선택] general - CrossCompile - [입력: arm-linux - gnueabi-] - save  
(6). make modules  
(7). 중간 혹은 마지막에 Error가 발생할 경우, 해당하는 파일을 'make menuconfig'로 접속하여 파일 삭제.  
(8). make modules [다시 한번]  
- ADB(Android Debug Bridge)   
(1). http://egloos.zum.com/kiringun/v/1354855  
(2). sudo apt-get install build-essential libncurses5-dev openjdk-7-jre openjdk-7-jdk bison   ##ADB파일 다운로드를 위한 모듈  
(3). tar -zxvf adb파일  
(4). Permission Error일 경우  
		sudo ./adb kill-server  
        sudo ./adb start-server  
        sudo ./adb devices  
[2-2]. 아직 찾고 있으나 발견 못함  
[2-3]. 마지막으로 최종 목표를 어떤 방향으로 잡을지 생각해봤을 때, 밑에 보시는 것과 같이 riverbed airpcap어댑터의 경우 시가 110만원에서 중고 60만원에 팔리고 있습니다. 해당 프로그램의 장점은 windows에서 이용할 수 있다는 것과 packet injection이 가능하다는 것 그리고 기존 packet분석 프로그램과 동일하게 DDos와 같은 페켓을 분석하는 것입니다. 이와 다르게 많은 기능은 들어가 있지 않지만 저렴하게 사용할 수 있는 것이 필요합니다. 예를 들어, 기업에서 특정 문서 혹은 파일을 감지하여 de-auth packet을 보내 arp-spoofing을 통해 분석할 수 있는 라즈베리파이로 통신하도록 하는 것도 괜찮을 것 같습니다.  

![11.jpg](C:\Users\ADMIN\Desktop\11.jpg)  
[airpcap 분석 UI: DDoS와 같은 유해 pacaket을 보여주기도 함]  
