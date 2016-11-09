[2016-11-10]
##1. AD-Hoc
(1).AD-HOC 구현 목적
(2).AD-HOC 추가 고려 사항 : 무선 랜 카드 +1
Raspberry A

    sudo service network-manager stop
    sudo ip link set wlan1 down
    sudo iwconfig wlan1 mode ad-hoc
    sudo iwconfig wlan1 channel 10
    sudo iwconfig wlan1 essid 'pjhs'
    sudo iwconfig wlan1 key 1234567890
    sudo ip link set wlan1 up
    sudo ip addr add 192.168.1.1/16 dev wlan1

Raspberry B

    sudo service network-manager stop
    sudo ip link set wlan1 down
    sudo iwconfig wlan1 mode ad-hoc
    sudo iwconfig wlan1 channel 10
    sudo iwconfig wlan1 essid 'pjhs'
    sudo iwconfig wlan1 key 1234567890
    sudo ip link set wlan1 up
    sudo ip addr add 192.168.1.2/16 dev wlan1

A와 B의 라즈베리파이 위에 TP-Link(Wlan1)를 AD-hoc모드로 변경한 후, 서로 주고 받을 key값을 '1234567890'으로 설정합니다.
하지만, 설정 단계에서 AD-hoc를 지원하는 무선 랜 카드가 한정되어 있습니다.[TP-Link722N: 지원O, TP-Link727N,IPTIME-N150UA: 지원X]
(3).결론 : AD-hoc 기능이 지원되는 무선 랜 카드에 한하여 접속 및 ping 가능.

##2.BlueTooth
(1).블루투스 구현 목적 : Wifi[ID/Pass], dot11decrypt[ID/Pass] 입력과 제어를 무선으로 하기 위함
(2).블루투스 추가 고려 사항 : App 제작 [terminal 제어]
-> 시중에 안드로이드로 제어할 수 있는 App도 있고, 만약 구현하게 된다면 함께 합숙이 필요한 시점

![1.jpg](C:\Users\ADMIN\Desktop\1.PNG)
![2.jpg](C:\Users\ADMIN\Desktop\2.PNG)

(3).블루투스 설정 방법
- 우리는 라즈베리파이 전용 칼리 리눅스에 블루투스 기능을 사용할 수 있도록 드라이브가 필요합니다.
- 기능이 없는 것은 아니고 kernel에서 실행될 수 있도록 드라이브를 크로스 컴파일합니다.
- kernel에 btsdio.c의 오브젝트 파일을 만들기 위해 ARM형식으로 크로스 컴파일합니다.
	[/usr/src/kernel/drivers/bluetooth : btsdio.c파일 위치]
    [/lib/modules/4.1.19-v7/kernel/drivers/bluetooth : 오브젝트 저장 위치]
- 이렇게 생성된 오브젝트 파일[드라이브][.ko파일]을 module이 있는 폴더로 옮겨 사용할 수 있도록 합니다.
- (여기서, 계속 오류 났던 이유는 매주 매일 업데이트 되고 변하는 칼리 버전의 Format을 한치 오차 없이 정확히 맞추지 않으면 invalid오류가 납니다.)

(4).결론 : 어제와 동일한 삽질 계속 진행


##3.ADB(Android Debug Bridge)
오늘 조사한 결론부터 말씀드리면 이 기술은 PC에서 안드로이드를 제어하거나 개발하는 경우에서 사용되는 것입니다.
SDK에 포함되어 있는 ADB데몬을 이용하여 PC에서 접속하는 방식입니다.