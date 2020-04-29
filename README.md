# 개요

```
Relay Module 과 Expressif 사의 ESP8266 을 Arduino IDE 를 이용하여 굽고,
이를 이용해서 출입문의 버튼에 연결해 Switch 가 High 가 되면 열리고, Low 가 되면 닫히도록 한다.
그리고 출입문에 설치한 안드로이드 디바이스에서 등록된 사용자의 얼굴 사진과 음성이
두개 다 인증에 성공하면 MQTT server 로 publish 되고
이 정보를 ESP 보드에서 받아서 Switch 가 작동해서 문이 열리는 구조이다.

이를 통해 코로나 바이러스로 인해 도래한 Untact 시대에 맞게 회사 사람들이 지문인식이나 비밀번호 입력 대신
손을 대지않고 출입을 할 수 있도록 하는데 의의가 있다.
추후 사업화 및 보안을 위해 모든 부분을 보안화된 프로토콜로 서버로 관리되게 할 예정이다.
현재 서버화된 부분은 화자인증 부분뿐이다.
```

## ESP8266 보드 세팅 (제품명: ESP-01)
<img src="https://github.com/Taehyung93/open_the_door/blob/master/1.png" width="50%" height="50%" title="ESP8266" alt="Ang"></img>

<ESP-01 USB 어답터>
```
위 사진에서처럼 Flash 모드로 하고 들어가야 작동한다.
Switch Slide 는 일반 ESP-01 USB 어댑터에 직접 연결해준 것이다.

Arduino 에서 ESP8266 보드 세팅 링크: https://tinyurl.com/ya54bggv
Arduino 에서 MQTT 라이브러리 설치 및 사용 가이드 링크: https://twinw.tistory.com/176

위 두 가지를 하고 여기에 올린 door_open_ESP8266.ino 를 다운받고,
본인의 Wifi ID,PWD, MQTT 서버 주소와 Topic 을 지정하고 
Arduino 에서 Compile 한 뒤 Upload 하면 이 부분은 쉽게 끝난다.
```

## Relay Module 세팅
<img src="https://github.com/Taehyung93/open_the_door/blob/master/4.png" width="50%" height="50%" title="ESP8266" alt="Ang"></img>
```
코드를 업로드한 ESP8266 모듈을 Relay Module 에 결합해준다.

ESP8266 모듈은 3.3V 동작 전압을 가지고 있다.
많은 수의 ESP-xx 모듈이 3.3V에서만 동작하므로 3.3V 전원이 필요하다.
UART 통신 라인도 3.3V로 동작하므로 아두이노 5V 동작전압의 보드들과 연동하려면
level converter 모듈을 이용하거나 저항을 이용해서 전압 분배 회로를 구성해줘야 한다.

그러므로 위 사진처럼 쇼트를 시키고, 저항을 달아주어 5V -> 3.3V 로 맞춰주어야한다.

전원은 일반 5V 용 충전기에 들어가는 선을 잘라서 연결시켜주면된다.

출입문은 아래 사진과 같이 진행해주면 된다. 현재 회사에 연결된 출입문 서비스는 세콤인데, 
인터넷을 전부 내려도 작동을 하는 것으로 보아 인터넷을 사용하지 않고 작동하거나,
자체적으로 망에 연결되어있는 것으로 보인다.
```
<img src="https://github.com/Taehyung93/open_the_door/blob/master/5.jpg" width="30%" height="40%" title="ESP8266" alt="Ang"></img>
<img src="https://github.com/Taehyung93/open_the_door/blob/master/6.jpg" width="30%" height="40%" title="ESP8266" alt="Ang"></img>

