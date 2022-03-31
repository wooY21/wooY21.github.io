---
layout: post
title: "Wi-Fi,RFID,Bluetooth 통신의 특징"
subtitle: "Communication Trait"
date: 2020-01-31 14:45:13 -0400
background: '/img/posts/06.jpg'
---

# __Wi-Fi(Wireless Fidelity)__
Wi-Fi란 *Wireless Fidelity*의 줄임말로 무선 데이터 전송 시스템이다. 무선 인터넷 공유기(AP)를 사용하여 각 기기에 연결되는 원리인데 유선 인터넷 통신을 무선 인터넷 공유기를 통해 무선 신호로 바꿔주어 무선 인터넷을 사용하는 원리라고 볼 수 있다. 연결 거리는 실내에서는 보통 10~30m까지 지원 가능하고 장애물이 많이 없는 야외에서는 100m까지도 통신이 가능하다. 하지만 분명한 단점도 존재한다.  
<br/>
 먼저, 무선 공유기의 신호 범위 내에서만 통신이 가능하고, 설치된 구조에 따라 신호의 범위가 좁혀져 사각지대가 발생할 수 있고 복합적인 무선 충돌로 인해 장치들간의 통신 장애가 발생되어 인터넷이 느려지거나 끊김 현상이 발생할 수 있다. 또한, 보안에 취약하여 해킹,정보 유출 가능성이 존재하고, 다른 통신 방식(Bluetooth,NFC 등)에 비해 전력 소모가 크다.  
 <br/>
![](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2FMjAyMTExMDFfNTMg%2FMDAxNjM1NzE0MjgyMzYw.ieLyKuIKZoGjaT5FZl6orPXI0K-dwnvoNOH0S8TMbM0g.ICePNjeQOoQwD2p3C4MnEZGO1m4heH13cKvZkYm6zfMg.JPEG.objective500%2F%25BF%25CD%25C0%25CC%25C6%25C4%25C0%25CC.JPG&type=sc960_832)

# __RFID(Radio-Frequency Identification)__  
RFID는 전파를 이용하여 먼 거리에서 정보를 인식할 수 있는 기술이다. RFID를 이용하기 위해서는 RFID 전용 태그와 판독기가 필요하다. 태그는 안테나와 __집적회로로__ 구성돼 집적 회로 안에 정보를 기록하고 안테나를 이용해 판독기로 정보를 송신하는 역할을 한다. RFID는 주파수에 따라 LFID,HFID,UHFID로 구분 된다. RFID는 반영구적으로 사용가능하고 원거리 인식과 공간 제약 없는 동작이 가능하다는 장점을 가지고 있는 반면 비용이 많이 들고 보안 상 개인 프라이버시가 침해될 수 있다. (같은 주파수를 읽는 판독기가 있으면 정보가 유출될 위험이 있음)  
* __집적회로__  
집적회로(IC)는 하나의 반도체 기판에 다수의 능동소자(ex. 트랜지스터)와 수동소자(ex. 다이오드,콘덴서,저항기 등)을 초소형으로 집적, 서로 분리될 수 없는 구조로 만든 완전한 회로기능을 갖춘 소자를 말한다.    

![](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2FMjAyMDA0MDVfMjUg%2FMDAxNTg2MDQxNDAwNDM0.a8biv3_3ltDNrq4Y02PQlVy_v56x3ctwXfC8c0JgWz8g.XHBV5mw0Q7eESldL52t-d6Udww5-WPPdd5wRZvAsRN8g.JPEG.hdjunkr%2FRFID%25BD%25C3%25BD%25BA%25C5%25DB%25B1%25B8%25BC%25BA%25BF%25E4%25BC%25D2.jpg&type=sc960_832)

# __Bluetooth__  
Bluetooth는 휴대폰,노트북,이어폰 등 휴대기기를 서로 연결해 정보를 교환하는 근거리 무선 기술 표준을 의미한다. 주로 10미터 내외의 초단거리에서 저전력 무선 연결이 필요할 때 쓰인다. Bluetooth의 무선 시스템은 __ISM__ 주파수 대역인 2400~2483.5 MHz를 사용한다. 이 중 위아래 주파수를 쓰는 다른 시스템들의 간섭을 막기 위해 2400MHz이후 2MHz,2483.5MHz이전 3.5MHz까지의 범위를 제외한 2402~2480MHz 총 79개의 채널을 사용한다.   
<br/>
 여러 시스템들과 같은 주파수 대역을 사용하는 Bluetooth특성상 시스템간 전파 간섭이 생길 우려가 있다. 이를 예방하기 위해 Bluetooth는 주파수 호핑이라는 방식을 취한다. 주파수 호핑이란 많은 수의 채널을 특정 패턴에 따라 빠르게 이동하며 데이터를 조금씩 전송하는 기법이다. 이 호핑 패턴이 Bluetooh 기기 간에 동기화 되어야 통신이 이루어진다. Bluetooth는 기기 간 마스터(Master)와 슬레이브(Slave) 구성으로 연결 되는데 마스터 기기가 생성하는 주파수 호핑에 슬레이브 기기를 동기화 시키지 못하면 두 기기 간 통신이 이루어지지 않는다. 이 방식을 사용하여 다른 시스템의 전파 간섭을 피해 안정적으로 연결 할 수 있다.
 <br/>  
하나의 마스터 기기에는 최대 7대의 슬레이브 기기를 연결할 수 있으며, __마스터<->슬레이브__ 통신은 가능하지만, __슬레이브<->슬레이브__ 통신은 불가능하다. Bluetooth를 지원하지 않는 기기에는 Bluetooth dongle(중계기)를 사용하여 Bluetooth가 가능하게 만들어 줄 수 있다.  
* ISM(Industrial Scientific and Medical)  
ISM이란 산업, 과학, 의료용으로 할당된 주파수 대역으로, 전파 사용을 허가 받을 필요가 없어 저전력의 전파를 발산하는 개인 무선기기에 많이 쓰인다. 아마추어 무선, 무선랜, 블루투스 등이 이 ISM대역을 사용한다.  

![](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2FMjAyMTA3MjhfMjcg%2FMDAxNjI3NDUzMjU5NjMw.dAI2arssPN2LjTHvw0y8B25Kxk9PYGoF56Zgqw4qpl8g.I55kh61jXzQSLwO8ShDcjOl-zqfPWsaFLaMv1CM8XPIg.JPEG.with_msip%2F%25BB%25E7%25C1%25F83.jpg&type=sc960_832)
