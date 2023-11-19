# 섹션 1
웹개발자라면 평생 HTTP 기반위에서 개발을 해야한다.  
그러니 언젠가 한번은 HTTP에 대해서 공부하고 정리를 해둬야한다.  

<br>

---
## 인터넷 통신
클라이언트와 서버가 같은 공간에 있다면 케이블을 연결해 메세지를 전달받을 수 있을 것이다.  
하지만, 서버와 클라이언트가 멀리 있다면 인터넷을 통해 메세지를 전달해야한다.  

인터넷을 통해 메세지를 전달하는 것은 단순하지 않다.  
무언가 복잡한 규칙을 통해서 메세지가 전달되는데, 그것을 **IP(인터넷 프로토콜)** 이라 한다.  

## IP(인터넷 프로토콜)의 역할
* 지정한 IP 주소(IP Address)에 데이터를 전달
* 패킷(Packet)이라는 통신 단위로 데이터 전달

메세지를 그냥 보내는 것이 아니라 IP 패킷을 이용해 보내는데  
<br>
<image style="width: 400px" src="https://github.com/Kimpossible94/TIL/assets/80395024/11e8aa1c-3113-43f5-a483-8000d7946a66"><br>
  
IP 패킷에는 출발지 IP(클라이언트의 IP 주소), 목적지 IP(서버 IP 주소), 메세지 등이 들어간다.  
그리고 이 패킷을 인터넷망에 던진다.  
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/80663405-adcb-43c2-bbd1-b79c7a5788e3"><br>
  
이제 인터넷망의 노드들이 던져진 패킷의 목적지에 도달하기 위해 서로 데이터를 전달한다.  
<details>
<summary>노드란 ?</summary>

#### 노드에 대한 간략한 설명  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/ab6587ef-ea09-4b25-83a0-ddf1538585ce"><br>
네트워크는 컴퓨터와 네트워크 장비를 *유무선의 전송 매체*로 연결하여 데이터를 전송하는 시스템이다.  
복잡한 네트워크 시스템을 단순화하면 네트워크는 그림과 같이 *전송 매체라는 선(또는 링크, Link)* 과 *컴퓨터와 네트워크 장비라는 점*들이 그물망처럼 연결된 것을 말한다.  
선을 여러 방향으로 분기시키는 각각의 점들을 **노드(Node, 분기점)** 라고 한다.  
  
다시 말해 **일반적으로 네트워크에 연결된 모든 물리적인 기기 또는 장치를 노드**라고 한다.    
즉, 네트워크 상에서 데이터를 주고받을 수 있는 PC, 노트북, 스마트폰 같은 컴퓨터와 라우터, 인터넷 공유기 같은 네트워크 장비가 각각 하나의 노드이다.   
노드는 네트워크에서 데이터를 전송하기 위해 연결된 기기이기 때문에 데이터를 보내는 송신지 또는 데이터를 받는 수신지 역할을 한다.  
따라서, 우편물을 주고받기 위해 송신지와 수신지의 주소가 필요한 것처럼 데이터를 주고받는 노드에도 다른 노드와 구별할 수 있는 고유한 주소가 필요하다.
따라서, 다른 노드와 구별되는 고유한 주소를 갖고 있는 노드를 네트워크에 연결된 주소가 있는 물리적인 장치라고 정의하기도 한다.  
MAC 주소라는 고유한 물리 주소를 갖고 있는 컴퓨터와 라우터가 네트워크의 대표적인 노드이다.  
<a href="https://better-together.tistory.com/74">노드 내용 출처</a>
</details>  

이렇게 데이터를 전달하다보면 목적지에 도달하게 된다.  
<br>
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/8aa1b25c-73b3-45b7-ab3f-112f0a3ea63d"><br>
  
이제 데이터를 받은 목적지에서 잘받았다는 OK라는 메세지를 담아서 다시 전달한다.  
그럼 다시 노드들이 데이터를 전달해서 메세지가 전달된다.  
  
## IP(인터넷 프로토콜)의 한계
1. 비연결성  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/376a4739-c2c6-4e3c-9a2a-88464ec1c515">
<br>

```
목적지에 있는 PC가 꺼진 상태여도 즉, 패킷을 받을 대상이 없거나
서비스 불능 상태여도 패킷이 전송된다는 문제가 있다.
클라이언트는 서버가 패킷을 받을 수 있는 상태인지 아닌지 모르기 때문에 패킷을 그냥 보내버린다.
```

2. 비신뢰성  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/c8a37014-b4e3-4e24-8e6d-395827cb0d9d">  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/948c06be-a9e8-45b6-90f6-468039225f69">
<br>

```
패킷의 용량이 크다면 패킷을 끊어서 보내는 데, 패킷을 여러개 보냈을 때 네트워크 지연등의 이유로
패킷이 순서대로 보내지지 않을 수 있다는 문제가 있다. 이런 문제가 생기면 데이터의 신뢰성이 떨어지게 된다.
또한, 중간에 있는 서버가 문제가 있거나 다른 문제로 인해 패킷이 소실이 되고 소실됬는지 알 수 없다.
그래서 도착한 패킷이 중간이 빠진 패킷인지 알 수 없기 때문에 마찬가지로 데이터의 신뢰성이 떨어진다.
```

이러한 문제를 해결하기 위한 것이 바로 **TCP, UDP** 이다.

---

<br>

---
## 인터넷 프로토콜 스택의 4계층  
![image](https://github.com/Kimpossible94/TIL/assets/80395024/62655dc4-bd93-4a37-ba6d-7a3a842b7aa0)  

~~~
4계층 : 애플리케이션 계층(Application Layer)  
사용자와 가장 가까운 계층으로, 사용자-소프트웨어 간 소통을 담당하는 계층이다.  
애플리케이션을 실행하기 위한 데이터 형식이 작성되는 계층이다.
프로토콜로는 HTTP, HTTPS, FTP, SSH, Telnet, DNS, SMTP 가 있다.
~~~
~~~
3계층 : 전송 계층(Transport Layer)
통신 노드 간 신뢰성 있는 데이터 전송을 보장하는 계층이다.
역캡슐화 과정에서, 포트 번호를 사용해 데이터를 정확한 애플리케이션에 전달하는 역할도 한다.
네트워크 액세스 계층과 인터넷 계층을 통해, 데이터가 목적지 기기까지 정상적으로 도착했다면,
전송 계층은 포트 번호를 사용해, 데이터를 목적지 기기 내 적절한 에플리케이션으로 전달한다.
프로토콜로는 TCP, UDP, RTP, RTCP 가 있다.
~~~
~~~
2계층 : 인터넷 계층(Internet Layer)
패킷을 최종 목적지까지 라우팅하는 계층이다.
프로토콜로는 IP, ARP, ICMP, RARP, OSPF 가 사용된다.
~~~

<details>
<summary>라우팅 ?</summary>
인터넷은 여러 네트워크의 연결로 구성되어있기 때문에 송신지에서 목적지까지 도달할 수 있는 경로가 여러개 있을 수 있다.
여기서 어느 하나의 올바른 경로를 선택하는 것이 라우팅(경로설정)이라 한다.
</details>  

~~~
1계층 : 네트워크 액세스 계층(Network Access Layer or Network Interface Layer)
데이터를 전기신호로 변환한 뒤, 물리적 주소인 MAC 주소를 사용해, 알맞은 기기로 데이터를 전달하는 계층이다.
프로토콜로는 Ethernet, Wi-Fi, PPP, Token Ring 과 같은 프로토콜이 사용된다.
~~~

## 인터넷 프로토콜 4계층의 캡슐화와 역캡슐화  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/ce82ab72-3823-4195-90b6-71ba3a0964ef">
  
데이터 전송시, 상위계층에서 하위계층으로 이동하고, 계층 이동마다 필요한 정보(헤더)가 추가된다.  
이를 캡슐화라고 한다.   
  
데이터 수신시, 하위계층에서 상위계층으로 이동하고, 계층 이동마다 추가된 헤더를 읽고 알맞은 행동을 취한후 헤더를 제거한다.  
이를 역캡슐화라고 한다.  

1. 프로그램이 데이터를 생성해서 OS계층에 전달
3. 전달된 메세지에 TCP 정보를 생성해서 씌움
4. TCP 정보 밖에 IP 정보를 생성해서 씌움
5. LAN 카드를 통해 전달 (이더넷 프레임을 통해 전달, MAC 주소등 물리적인 정보를 포함하고 있다.)

## TCP의 특징  
전송 제어 프로토콜  
* 연결지향 - 상대 서버와 연결이 되었는지 안되었는지 확인 후 메세지를 보낸다. (TCP 3 way handshake)
* 데이터 전달 보증
* 순서 보장
* 위의 특징으로 신뢰할 수 있는 프로토콜이며, 현재는 대부분 TCP를 사용한다.

### TCP 3 way handshake  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/63e547ba-29d3-4bfb-b974-296a705a700c">  
  
1. 클라이언트에서 서버로 연결해달라는 요청인 SYN을 보낸다.
2. 요청을 수락한다는 의미인 ACK를 보내면서 동시에 클라이언트에게 연결을 요청하는 SYN을 보낸다.
3. 마지막으로 클라이언트도 수락한다는 ACK를 보낸다.
4. 이렇게 연결을 서로 확인 후 데이터를 전송한다. (SYN을 보낸 후 응답이 없다면 데이터를 전송하지 않는다.)
*최근에는 최적화가 되어서 마지막으로 클라이언트가 ACK를 보낼 때 데이터도 전송을 한다.*  
*물리적으로 연결되었다고 하지않고, 논리적으로 연결되었다고 한다.*
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/cfe386f0-7eee-4921-bbee-159f6173cf66">   
  
TCP 세그먼트 안에는 전송 제어, 순서, 검증 정보등이 있어서 아래와 같은 동작이 가능하다.  
  
### 데이터 전달 보증  
데이터 전송을 잘 받았는지에 대한 응답을 해주므로 데이터 전달이 잘 되었는지 알 수 있다.  

### 전달 보장  
패킷1 -> 패킷2 -> 패킷3 이렇게 보냈는데 서버에는 패킷1 -> 패킷3 -> 패킷2 이렇게 전달되었을 때,  
서버에서 검증 후 다시 전달을 요청한다.  
  
## UDP의 특징  
사용자 데이터그램 프로토콜  
* 연결지향 - TCP 3 way handshake X
* 데이터 전달 보증 X
* 순서 전달 보증 X
* 단순하고 속도가 빠름
* IP(인터넷 프로토콜)와 거의 같고, 거기에 PORT와 체크섬 정도만 추가되었다.
---

<br>

---
## PORT  
IP주소만 가지고 있다면, 여러개의 프로그램에서 동시에 요청을 보낼 때 어디에서 보냈는지 알 수 없다.  
예를 들어 클라이언트가 게임을 하며 음성채팅을 하고 있다면, 하나의 클라이언트 PC가 여러개의 서버와 통신을 해야한다.  
이럴 때 응답받은 패킷이 어디에서 보낸 패킷인지 IP주소만을 가지고는 알 수 없다.  
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/cfe386f0-7eee-4921-bbee-159f6173cf66">   
  
이 문제를 해결하기 위해 TCP/IP 패킷에는 사진과 같은 정보가 있다.  
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/f54c4b75-6220-4860-90f1-d088764684aa">   

위의 사진처럼 같은 IP내에서 프로세스를 구분하는 것이 포트이다.  
패킷안에 출발지 IP/PORT, 목적지 IP/PORT 에대 한 정보가 있기 때문에 프로세스를 구분해 통신할 수 있다.  
```
0 ~ 65535 사이의 숫자로 포트를 할당가능하다.
0 ~ 1023 사이의 숫자는 잘 알려진 포트이므로 사용하지 않는 것이 좋다.
20, 21 : FTP
23 : TELNET
80 : HTTP
443 : HTTPS
```

## DNS  
IP주소는 외우기 쉽지않다. 한 두개의 IP 주소를 외우는 것이 아니라 통신하려는 서버의 모든 IP주소를 외우고 알고 있어야한다.  
심지어 IP주소는 변경될 수 있으므로, IP 주소를 외운다고해도 변경될 때마다 다시 기억해야한다.  

이를 해결하기 위한 DNS (Domain Name System)이 있다.  
DNS는 전화번호부 같은 서버(?)라고 이해하면 된다.  
예를 들어 google.com 라는 도메인 명으로 DNS 서버에 요청을하면 200.200.200.2 라는 특정 IP주소를 반환해주고  
클라이언트는 반환받은 아이피에 요청을 보낸다.  
추후 IP가 바뀌어도 도메인 명만 알고있으면 되므로 위에서 언급한 문제가 해결된다.  

<br>
<br>
<br>
<br>

# 섹션 2
URI와 웹브라우저의 요청 흐름  

<br>

---
## URI  
Uniform Resource Identifier  

### URI, URL, URN   
  
우선 URI라는 가장 큰 개념이 있다.  
URI는 Resource Identifier로 자원을 식별하는 것을 말한다.  
₩₩₩
U (Uniform) : 리소스를 식별하는 통일된 방식
R (Resource) : 자원, URI로 식별할 수 있는 모든 것(제한없음)
I (Identifier) : 다른 항목과 구분하는데 필요한 정보
₩₩₩

식별하는 방법은 크게 **URL**과 **URN**이 있다.  

URL은 Resource Locator, URN은 Resoure Name이다.  
<br>

***URL***  
리소스가 있는 위치를 지정  

<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/fa9afc7b-7596-48c4-b116-0b344ea8db8d">  
  
~~~
scheme:[//[user[:password]@]host[:port]][/path][?query][#fragment]
  
scheme : 어떤 방식으로 자원에 접근할 것인가를 나타냄 웹에서는 http 또는 https를 사용
user와 password : (서버에 있는) 데이터에 접근하기 위한 사용자의 이름과 비밀번호 (생략가능, 거의 사용하지 않음)
host와 port : 접근할 대상(서버)의 호스트명과 포트번호 (포트는 생략가능 : 생략시 일반적으로 http는 80, https는 443)
path : 접근할 자원의 경로, 계층적 구조로 되어있다. (/example/home/file1.jpg) (생략가능)
query : 접근할 대상에 전달하는 추가적인 정보 (파라미터, 생략가능)
fragment : 메인 리소스 내에 존재하는 서브 리소스에 접근할 때 이를 식별하기 위한 정보 (생략가능)
~~~

***URN***  
리소스에 이름을 부여  

~~~
URN은 URI의 표준 포맷 중 하나로, 이름으로 리소스를 특정하는 URI이다.
http와 같은 프로토콜을 제외하고 리소스의 name을 가리키는데 사용된다.
요즘엔 사용하지 않기 때문에 정의정도만 알아두면 될 것이다.
~~~

## 웹 브라우저의 요청 흐름  
내가 주소창에 https://www.google.com/search?q=hello&hl=ko  
이렇게 요청을 보낸다고 했을 때 흐름은 아래와 같다.  

~~~
1. www.google.com로 DNS를 조회해 200.200.200.2라는 IP를 반환받는다.
2. port 번호는 https 이므로 443이 된다. 이렇게 IP주소 정보와 port 정보를 찾는다.
3. 애플리케이션에서 HTTP 요청 메세지를 생성한다.
4. IP, PORT 정보를 가지고 애플리케이션에서 SOCKET 라이브러리를 통해서 TCP/IP연결을 한다.(3way-handshake)
5. OS 계층에 데이터를 전달한다.
6. TCP/IP 에서 데이터에 패킷을 씌운다. (HTTP 메세지도 포함)
7. 인터넷망으로 패킷정보를 던짐


8. 서버에서는 HTTP 메세지를 해석하고 HTTP 응답 메세지를 만든다.
9. 그리고 똑같이 패킷을 씌우고 다시 재전송한다.
~~~
---  

<br>
<br>
<br>
<br>

# 섹션 3
HTTP 기본

<br>

---
## 모든 것이 HTTP  
HyperText Transfer Protocol  

요즘은 HTTP 메세지에 거의 모든 것을 담아서 전송한다.  
HTML, TEXT, IMAGE, 음성, 영상, 파일, JSON, XML 등 거의 모든 것을 담아서 전송하고  
심지어는 서버간의 데이터를 주고 받을 때도 대부분 HTTP를 사용한다.  

**HTTP 스펙**  
많은 스펙 중 우리에게 가장 중요한 스펙은 HTTP/1.1이다.  
HTTP/1.1에 대부분의 기능이 들어있고 HTTP/2, HTTP/3는 대부분 성능 개선에 초점이 맞춰져 있기 때문이다.  
  
**기반프로토콜**  
HTTP/1.1, HTTP/2는 TCP 프로토콜을 기반으로 작동  
HTTP/3는 UDP 프로토콜을 기반으로 작동  

현재는 HTTP/1.1을 주로 사용하고, HTTP/2와 HTTP/3도 점점 증가하는 추세이다.  

**HTTP 특징**  
* 클라이언트-서버 구조
* 무상태 프로토콜, 비연결성
* HTTP 메세지를 통해서 통신
* 단순하고 확장이 가능
  
## 클라이언트-서버 구조  

<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/dd074797-a5c7-4d9b-8c68-8e17d6062738">  
  
~~~
클라이언트-서버 구조로 분리하면 각각 독립적으로 진화가 가능하다.
클라이언트는 복잡한 데이터, 비즈니스 로직을 다룰 필요없이 UI를 어떻게 그릴지만에 집중할 수 있고
서버는 비즈니스 로직에 집중할 수 있기 때문이다.
~~~

## 무상태 프로토콜
stateful과 stateless의 차이  
stateful은 서버가 클라이언트의 상태를 보존하는 것이고, stateless는 상태를 보존하지 않는 것이다.  
HTTP에서는 통신이 끝나면 클라이언트의 상태를 보존하지 않는데,  
클라이언트의 상태와 관계없이 동작하므로 **스케일링**에서 유리하다는 장점이 있다.  

<details>
<summary>스케일링</summary>
클라이언트가 집중되는 경우 서버의 부하 발생을 완화시키기 위해서 서버의 개수를 늘리거나 스펙을 변경하는 것
</details>  

**실무적인 한계**  
모든 것을 무상태로 설계할 수가 없다.  
예를 들어 로그인같은 경우에는 로그인 했다는 상태를 유지해야하기 때문에 브라우저의 쿠키와 세션을 이용한다.  
이런 경우 브라우저의 쿠키와 세션이 날아가면 로그인 정보가 날아간다는 한계점이 있다.  
결과적으로 상태 유지는 어쩔 수 없는 경우에 최소한으로만 사용하자.  

## 비연결성  
연결을 한 번하고 종료하기 전까지 계속해서 연결이 되어있다면 서버의 자원을 계속해서 잡아먹을 것이다.  
HTTP는 요청을 하고 응답을하며 연결을 끊어버린다.  
이렇게하면 자원을 연결하고 응답할때까지만 할당하면 되기 때문에 자원에 대한 낭비를 막을 수 있다.  

**한계점**  
요청마다 TCP/IP 연결을 새로 맺어야하므로 3way-handshake하는 시간이 추가된다.  
지금은 HTTP 지속 연결로 문제를 해결했다.  
HTTP/2와 HTTP/3에서는 더 많이 최적화를 했다.  

## HTTP 메세지  
HTTP 메세지는 Request(요청)과 Response(응답) 2가지가 있다.  

**HTTP 메시지 구성**  
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/85934e0f-d7a9-45d0-af42-f66a857fde50">  

> 1. 시작라인  
> 시작라인은 크게 request-line과 status-line으로 나뉜다.  
> request-line에는 **Method** [공백] **request-target** [공백] **HTTP-version** **CRLF** [엔터]  
> 이렇게 들어간다.  
>> 1-1. Method는 GET, POST, PUT, DELETE 등이 있다.  
>> 1-2. request-target(요청대상)은 [search?q=hello] 이런식으로
>> 절대경로와 쿼리를 합쳐서 들어간다.(쿼리는 생략가능)
>> 1-3. 마지막에는 HTTP/1.1 같은 버전을 넣어준다.
>> HTTP 요청 메세지까지는 이렇게 들어가고 HTTP 응답 메세지에서는 status-line이 추가된다.
>> status-line에는 **HTTP-version** [공백] **status-code** [공백] **status text**
>> 이렇게 들어간다.  
>  
> 2. HTTP Header  
>> HTTP Header에는 HTTP 전송에 필요한 모든 부가정보가 들어있다.  
>> 메시지 바디의 정보, 메시지 바디의 크기, 압축 여부, 인증 정보 등 많은 정보가 들어간다.  
>  
> 3. Messasge Body  
>> 실제 전송할 데이터가 들어간다.  
>> HTML 문서, 이미지, JSON 등 byte로 표현할 수 있는 모든 정보를 Body에 담아 전송할 수 있다.  

---

<br>
<br>
<br>
<br>

# 섹션 4
HTTP 메서드

<br>

---  
## HTTP API를 만들어보자  
회원에 관련된 API를 설계한다고 가정하고 아래와 같이 URI를 만들었다.  
```
회원 목록 조회 : read-member-list
회원 조회 : read-member-by-id
회원 등록 : create-member
회원 수정 : update-member
회원 삭제 : delete-member
```
이제 이렇게 만든 것이 정말 좋은 URI설계인가에 대해서 고민을 해봐야한다.  

우선, 이 설계에서 리소스에 대한 개념부터 생각해보자.  
여기에서 리소스는 '회원' 그 자체이지 회원에 대한 행동 (회원 조회, 등록, 수정, 삭제)가 아니다.  
그래서 URI에서는 회원이라는 리소스를 식별하는 행동에 중점을두고 리소스에 대한 행동은 모두 배제해야한다.  
애초에, URI 라는 것이 리소스를 식별하는 방법을 말하는 단어이기 때문이다.  

그럼 이제 다시 설계를 해보면 아래처럼 할 수 있다.  
```
회원 목록 조회 : /members
회원 조회 : /members/{id}
회원 등록 : /members/{id}
회원 수정 : /members/{id}
회원 삭제 : /members/{id}
* 계층 구조상 상위를 컬렉션으로 보고 복수단어를 사용.
```
그럼 이제 여기서 또 문제가 생긴다.  
다시 URI 설계를 잘해서 URI는 리소스를 식별하는 것에 집중했는데 이제 그 리소스에 대한 행동이 없다.  
그 행위에 대한 구분은 **HTTP 메서드**를 사용한다.  
  
## HTTP 메서드  
HTTP 메서드에는 GET, POST, PUT, PATCH, DELETE 등이 있고, 이 5가지를 주로 사용한다.  
1. GET : 리소스 조회
2. POST : 요청 데이터 처리, 주로 등록에 사용
3. PUT : 리소스를 대체, 해당 리소스가 없으면 생성
4. PATCH : 리소스 부분 변경
5. DELETRE : 리소스 삭제
그 외로는 HEAD, OPTIONS, CONNECT, TRACE 가 있다.

  
**GET 메서드**  
```
GET /search?q=hello HTTP/1.1  
Host: www.google.com  

* 리소스 조회
* 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
* 메세지 바디를 사용해서 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않는다.
```  

**POST 메서드**  
```
POST /member HTTP/1.1  
Content-Type: application/json
{
  "username": "hello",
  "age": 20
}

* 메시지 바디를 통해 서버로 요청 데이터 전달
* 요청 데이터 처리
  * 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
* 주로 신규 리소스 등록 또는 프로세스 처리에 쓰인다.
```  

**POST는 요청 데이터를 어떻게 처리할까?**
```
* 스펙: POST 메서드는 대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청합니다.
  (이해하기 어려운 말이니 예제를 보자.)
* 게시판, 블로그 또는 유사한 기사 그룹에 메시지 게시
  - 예) 게시판 글쓰기, 댓글 달기 등
* 서버가 아직 식별하지 않은 새 리소스 생성
  - 예) 신규 주문 생성
* 기존 자원에 데이터 추가
  - 예) 한 문서의 끝에 내용 추가하기

정리하면, 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스 마다 따로 정해야 한다.
즉, 정해진 것이 없다.
```

**POST 정리**
```
결과적으로 POST 아래와 같은 상황에 사용한다.
1. 새 리소스 생성
2. 요청 데이터 처리
3. 다른 메서드로 처리하기 애매한 경우
  - 예) JSON으로 조회 데이터를 넘겨야 하는데 GET 메서드를 사용하기 어려운 경우 (GET의 body를 잘 허용하지 않기때문에)
        이런 경우에는 조회이지만 POST를 사용해야한다.
```

**PUT 메서드**  
```
PUT /member/100 HTTP/1.1  
Content-Type: application/json
{
  "username": "hello",
  "age": 20
}

* 리소스를 대체
  * 리소스가 있으면 대체
  * 리소스가 없으면 생성
* 중요! 클라이언트가 리소스의 위치를 알고 식별해 URI를 지정한다. (POST와 차이점)
  - /member/100 이렇게 정확한 위치를 알고 지정한다.
* 중요! PUT은 기존 리소스를 완전히 대체하는 것이므로 부분만 변경할 때는 PATCH를 사용해야 한다.
```  

**PATCH 메서드**  
```
PATCH /member/100 HTTP/1.1  
Content-Type: application/json
{
  "age": 20
}

* 리소스 부분 변경
* PATCH를 지원하지 않는 경우가 있다. 이런 경우에는 무적의 POST를 사용하자 !
```  

**DELETE 메서드**  
```
DELETE /member/100 HTTP/1.1  
Content-Type: application/json

* 리소스 삭제
```

**HTTP 메서드의 속성**  

<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/dfe53a4c-f754-460b-a950-8aab09d14341">  
  
HTTP 메서드 속성에는 안전(Safe Methods), 멱등(Idempotent Methods), 캐시가능(Cacheable Methods)이 있다.  

***안전***
```
안전은 호출해도 리소스가 변경하지 않는 것을 말한다.
GET 메서드의 경우 단순한 호출이기 때문에 리소스가 변하지 않으므로 안전한 메서드에 해당한다.
이에 반해서 POST, PUT, PATCH, DELETE 같은 경우에는 리소스가 변경된다.

* GET을 계속해서 호출하면 서버에 로그가 쌓여서 장애가 발생할 수 있지 않을까 ?
  - 안전은 해당 리소스만 고려하기 때문에 그 외에 것들은 고려하지 않는다.
```

***멱등***
```
멱등의 개념은 다음과 같다.
수학이나 전산학에서 연산의 한 성질을 나타내는 것으로, 연산을 여러번 적용하더라도 결과가 달라지지않는 성질
즉, "동일한 연산을 여러 번 수행하더라도 동일한 결과가 나타나야 한다는 것"이다.

GET : 몇 번을 호출해도 동일한 결과가 조회된다.
PUT : 결과를 대체하기 때문에 몇 번을 호출해도 동일한 결과가 나온다.
  - 헷갈릴 수 있는데 예를 들어 /member/100 으로 {"name": "hello"}를 계속 보낸다면
    몇 번을 보내든 덮어씌우기 떄문에 리소스가 동일한 상태를 유지한다.
DELETE : 결과를 삭제한다. 때문에 몇 번을 호출해도 삭제된 결과는 똑같다.
PATCH : PATCH는 얼핏보면 멱등한 것 같지만, 멱등하지 않다.
  - /member/100로 {"name": "hello"} 이렇게 계속 보낸다면 상태가 같기 때문에 멱등하게 보이지만
    /member/100에 PATCH를 통해 name 필드에 값을 추가하는 요청을 보낸다면, {"name": "hello"} {"name": "hello hello"}
    이런식으로 되기 때문에 멱등하지 않다.
POST : POST는 당연하게 멱등하지 않다.
  - 데이터를 생성하는 POST 요청을 계속 보낸다면 리소스가 동일한 상태이지 않다.

단, 멱등은 외부 요인으로 인한 리소스 변경은 고려하지 않는다.
오로지 나만 동일한 요청을 보냈을 때만 고려한다.
사용자 A : GET => userName: hello, age: 20
사용자 B : PUT => userName: hi
사용자 A : GET => userName: hi, age: 20
이런 경우 사용자 A는 바뀐 데이터가 조회되지만, 멱등성을 따질 때 이런 경우까지는 생각하지 않는다.
```

***멱등은 왜 필요한가?***
```
HTTP 멱등성이 필요한 이유는 요청의 재시도 때문이다.
HTTP 요청이 멱등하다면, 요청이 실패한 경우에 재시도 요청을 하면 된다.
하지만 HTTP 요청이 멱등하지 않다면, 리소스가 이미 처리된 상태에서 중복요청을 보낼 수 있다.
예를 들어 이미 결제된 요청인데, 중간에 연결이 끊겨서 다시 결제 요청을 보내서 문제를 일으킬 수 있는 것이다.
```

***캐시가능***
```
js, css, 이미지 같은 정적 컨텐츠는 데이터양이 크고 변경될 일이 적기때문에
정적 컨텐츠를 요청하고 나면 브라우저에서 요청을 캐시해두고, 동일한 요청이 발생하면 서버로 요청하지 않고 캐시된 데이터를 사용한다.

GET, HEAD, POST, PATCH 캐시가능
실제로는 GET, HEAD 정도만 캐시로 사용
  - 캐시를 구현하려면 Key가 맞아야하는데 POST, PATCH는 body안의 내용까지 고려해야하기 때문에 구현이 어렵다.
```

---  


<br>
<br>
<br>
<br>

# 섹션 5
HTTP 메서드 활용

<br>

---
## 클라이언트에서 서버로 데이터 전송  

### 클라이언트에서 서버로 데이터 전송
데이터의 전송방식은 크게 2가지 이다.  
1. 쿼리파라미터를 이용한 전송방식  
   - GET  
   - 주로 정렬 필터  
2. 메시지 바디를 이용한 전송방식  
   - POST, PUT, PATCH  
   - 리소스 변경 또는 리소스 등록  
  
### 4가지 상황을 통한 데이터 전송 방법 알아보기
1. 정적 데이터 조회 (쿼리 파라미터 미사용)  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/1c75a9fe-755b-4677-a5f0-419b705e0f3d">  
  
```
* 단순히 star.jpg라는 이미지의 리소스를 클라이언트에게 전달해준다.
```

2. 동적 데이터 조회 (쿼리 파라미터 사용)  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/cd052fbb-55ea-490d-ba01-a70cb8571cec">

```
* 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
```

3. HTML Form 데이터 전송  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/3cea843b-df93-4bb4-a258-3db4bb86973d">

```
* 전송 버튼을 누르면 웹브라우저가 Form 데이터를 읽어서 오른쪽처럼 HTTP 메시지를 생성해준다.
* method를 get으로 바꾸면 쿼리 파라미터로 보내지는데, 리소스가 변경되는 요청은 GET으로 하면 안된다.
* 한글 같은게 들어가 있는 경우 인코딩이 되어서 요청값이 넘어간다.
* HTML Form 전송은 GET, POST만 지원한다.
```
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/ba8bc944-d879-4e3e-b624-13d67a205be9">   
  
```
* 사진과 같이 파일이 같이 전송된다면 multipart/form-data를 사용해야 한다.
* multipart/form-data를 사용하면 웹브라우저가 boundary라는 것을 만들어서 데이터를 자른다.
```

4. HTTP API 전송
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/6b6a4f0c-90e8-4721-9b65-5af1ff10366a">  


```
* API에서 요구하는 데이터를 만들어서 요청하면 된다.
* 서버 to 서버 백엔드 시스템 통신에서 사용
* HTML에서 From 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)
* Content-Type : application/json을 주로 사용 (사실상 표준)
```

### HTTP API 설계 예시
1. 회원 관리 시스템  
```
* 회원 목록 : /members => GET
* 회원 등록 : /members => POST
* 회원 조회 : /members/{id} => GET
* 회원 수정 : /members/{id} => PATCH, PUT, POST
* 회원 삭제 : /members/{id} => DELETE

회원 관리 시스템은 위처럼 설계하면 된다.

회원 등록시 POST로 데이터를 넘기면 서버가 회원을 만들고 리소스 URI(ex. /members/100)를 만들어 준다.
그리고 HTTP 응답 메세지 Header에 Location: /members/100 이런식으로 데이터를 클라이언트에게 넘겨준다.
이렇게 서버가 관리하는 리소스 디렉토리를 "컬렉션(Collection)"이라고 한다.
```  

2. 파일 관리 시스템  
```
* 파일 목록 : /files => GET
* 파일 조회 : /files/{fileName} => GET
* 파일 등록 : /files/{fileName} => PUT
* 파일 삭제 : /files/{fileName} => DELETE
* 파일 대량 등록 : /files => POST

파일 관리 시스템은 위처럼 설계하면 된다.
파일의 경우 동일한 이름으로 파일이 있다면 덮어씌워야 하므로 PUT을 쓴다.

회원과 다르게 파일을 등록할 때 클라이언트가 fileName을 직접 넘겨주는데,
클라이언트가 리소스 URI를 알고 관리해야 한다는 뜻이다.
이렇게 클라이언트가 관리하는 리소스 저장소를 "스토어(Store)"라고 한다.
```

3. HTML FORM을 사용한 회원 관리 시스템  
```
HTML FORM은 GET과 POST만 지원한다.

* 회원 목록 : /members => GET
* 회원 등록 폼 : /members/new => GET
* 회원 등록 : /members/new, /members => POST
회원 등록 폼을 불러올 때는 /members/new
등록할 때는 /members/new 또는 /members를 사용

* 회원 조회 : /members/{id} => GET
* 회원 수정 폼 : /members/{id}/edit => GET
* 회원 수정 : /members/{id}/edit, /members/{id} => POST

* 회원 삭제 : /members/{id}/delete => POST

GET, POST만 지원하므로 위와 같은 설계가 나온다. (제약이 있음)
제약을 해결하기 위해 동사로 된 리소스 경로가 사용되는데, 이런것을 컨트롤 URI라고 부른다.
컨트롤 URI는 HTTP 메서드로 해결하기 애매한 경우에 사용한다. (실무에서 많이 사용된다.)
(최대한 리소스라는 개념을 가지고 URI를 설계하고 그게 안될 때 컨트롤 URI를 대체재로 사용해야한다.)
```

4. 리소스 종류   
```
* 문서(document)
  - 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
  - ex. /members/100, /files/star.jpg
* 컬렉션(Collection)
  - 서버가 관리하는 리소스 디렉터리
  - 서버가 리소스의 URI를 생성하고 관리
  - ex. /members
* 스토어(Store)
  - 클라이언트가 관리하는 리소스 저장소
  - 클라이언트가 리소스의 URI를 알고 관리
  - ex. /files
* 컨트롤러, 컨트롤 URI
  - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
  - 동사를 직접 사용
  - ex. /members/{id}/delete
```  

---


<br>
<br>
<br>
<br>

# 섹션 6
HTTP 상태 코드

<br>

---   
## HTTP 상태코드  
HTTP 상태코드는 크게 5가지로 나눠진다.  
```
1. 1xx : 요청이 수신되어 처리중 (거의 사용되지 않음)
2. 2xx : 요청 정상 처리
3. 3xx : 요청을 완료하려면 추가 행동이 필요
4. 4xx : 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음
5. 5xx : 서버 오류, 서버가 정상 요청을 처리하지 못함
```
정리하던 데이터 날아감... 다시 듣고 작성 해야함...

---


<br>
<br>
<br>
<br>

# 섹션 7
HTTP 헤더 - 일반헤더  

<br>

---   
## HTTP 헤더 개요  

<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/42826a8d-fb47-4c2e-a9a4-370685c3311f">  

RFC7230에서는 표현이라는 것이 나오는데 요청이나 응답에서 전달할 실제 데이터를 말하며, 표현 메타데이터 + 표현 데이터로 이루어져 있다.  
메시지 본문(message body)을 통해 표현 데이터 전달한다. (메시지 본문 = 페이로드(payload))  

표현 헤더는 표현 데이터를 해석할 수 있는 정보를 제공한다.  

## 표현  
표현 헤더는 표현 데이터를 해석할 수 있는 정보를 제공하는데 아래와 같은 정보를 제공한다.  

* Content-Type: 표현 데이터의 형식  
  - text/html; charset=utf-8, application/json, image/png ...  
* Content-Encoding: 표현 데이터의 압축 방식  
  - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가  
  - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제  
  - gzip, deflate, identity ...  
* Content-Language: 표현 데이터의 자연 언어  
  - ko, en, en-US ...  
* Content-Length: 표현 데이터의 길이  
  - 바이트 단위  
  - Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨  

## 협상  
협상은 클라이언트가 선호하는 표현을 서버에 요청하는 것을 말한다. (서버가 못줄 수도 있다.)  
협상 헤더는 요청시에만 사용한다.  
* Accept: 클라이언트가 선호하는 미디어 타입 전달 
* Accept-Charset: 클라이언트가 선호하는 문자 인코딩 
* Accept-Encoding: 클라이언트가 선호하는 압축 인코딩 
* Accept-Language: 클라이언트가 선호하는 자연 언어

### 예시  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/9ecd1b3a-a3c2-472c-8a96-dffe82088b13">   
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/d9dd6c21-2791-4650-8ccc-7e2151dfa249">  
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/a8f33fca-6b9d-4cb0-87e5-59b067e7a247">  
  
```
적용전에는 외국어 사이트의 이벤트 페이지를 요청하면 서버에서는 기본값은 영어로된 페이지를 반환해준다.
하지만, Accept-Language를 한국어로 요청하면 한국어로된 페이지를 서버에서 리턴해준다.

마지막으로 다중언어를 지원해주는 페이지이지만 영어, 독일어를 지원하고 한국어를 지원하지 않는 사이트에서
한국어를 지원하지 않는다면 영어로 되어있는 페이지를 선호하는 상황이다.
이 상황에서는 서버에 ko로 보낸다면 기본값일 독일어로된 페이지를 리턴할 것이다.
마지막처럼 복잡한 상황에서 필요한 것이 "우선순위"이다.  
```  

## 협상과 우선순위  
우선순위를 결정하기 위해 Quality Values를 사용한다.  
0~1사이의 숫자를 사용하며, 클수록 높은 우선순위이다. (생략하면 1)  

```
아래처럼 Accept-Language을 요청했을 때
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7

우선순위는 다음과 같다.
1. ko-KR;q=1 (q생략)
2. ko;q=0.9
3. en-US;q=0.8
4. en;q=0.7

마지막같은 경우에서는 Accept-Language에 독일어(de)는 없고 en이 있기때문에 영어로된 페이지를 리턴해준다.  
```

**구체적인 것이 우선이다.**  
```
아래처럼 Accept(미디어 타입)를 요청했을 때
Accept: text/*, text/plain, text/plain;format=flowed, */*

우선순위는 다음과 같다.
1. text/plain;format=flowed
2. text/plain
3. text/*
4. */*
```

## 전송 방식  
전송 방식에는 아래의 4가지 방식이 있다.  

* 단순 전송
```
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423 
<html>
 <body>...</body>
</html>

길이를 알 수 있을 때 사용한다.
한 번에 요청하고 서버에서 한 번에 쭉 받는다.  
```

* 압축 전송  
```
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Encoding: gzip 
Content-Length: 521
lkj123kljoiasudlkjaweioluywlnfdo912u34ljko98udjkl

서버에서 압축을 해서 전송한다.
이 경우에는 Content-Encoding로 뭘로 압축되어있는지 알려준다.
이 경우의 Content-Length는 압축된 크기를 말한다.
(Content-Length를 압축된 크기로 알려줘야 메세지 전송의 끝을 알 수 있음.)
(https://www.oreilly.com/library/view/http-the-definitive/1565925092/ch15s02.html)
```

* 분할 전송  
```
HTTP/1.1 200 OK
Content-Type: text/plain
Transfer-Encoding: chunked 
5
Hello
5
World
0
\r\n

chunked(덩어리)로 보낼거라고 Transfer-Encoding에 명시해준다.
5byte의 Hello를 서버에서 보내고,
5byte의 World를 서버에서 보내고,
마지막으로 전송이 끝났다는 것을 보낸다.

이 경우에는 데이터가 어떤 데이터를 보낼지 모르기때문에 Content-Length를 보낼 수 없다.
```

* 범위 전송  

<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/8e82ca06-0776-4d18-84a2-2a3eb752ccaf">  


```
Content-Range로 범위를 지정해서 요청을 하는 것을 말한다.
예를 들어 이미지를 다운받다가 중간에 끊겼을 때 다시 요청을 보내 처음부터 받기보다는 중간에 끊어진 부분부터
다운로드 받을 수 있도록 범위 전송을 보내는 것.
```

## 일반 정보  
* From : 유저 에이전트의 이메일 정보
* Referer : 요쳥된 웹페이지의 이전 주소
  - 유입 경로 분석 가능
  - referrer라는 단어의 오타인데 오치면 서버에서 파싱을 못하기때문에 못바꿈
* User-Agent : 클라이언트 애플리케이션 (=유저 에이전트) 정보
  - 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능 
* Server : 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
  - HTTP 요청을 보내면 중간에 여러 프록시서버를 거치게 된다. 그런 서버를 제외하고 진짜 요청이 있는 서버를 말한다.
  - 응답에서 사용
* Data : 메시지가 발생한 날짜와 시간

## 특별한 정보  
* Host: 요청한 호스트 정보(도메인)  
  <image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/e1708f21-d125-45ce-8738-1bec18228410">  
  - 하나의 서버가 여러 도메인을 처리해야할 때 사용한다. (하나의 서버안에 여러개의 다른 도메인이 구동)
  - 필수값
  - 하나의 서버가 여러 도메인을 처리하면 200.200.200.1 에 hello 라는 요청을 보냈을 때 IP로 요청을 보내므로 어떤 도메인에서 처리해야할지 알 수 없다.
  - Host가 있다면 어느 도메인에서 처리해야하는지 알 수 있기때문에 처리가 가능하다.
* Location: 페이지 리다이렉션
* Allow: 허용 가능한 HTTP 메서드
* Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

## 인증  
* Authorization: 클라이언트 인증 정보를 서버에 전달
  - OAuth 등 여러 인증 방식이 있기때문에 그에 대한 값을 넣어준다.
  - HTTP 헤더의 Authorization는 어떤 인증방식인지는 모르고 일단 헤더를 제공해준다.
* WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의

## 쿠키  
* Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
* Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

### Stateless
  - HTTP는 무상태(Stateless) 프로토콜이기 때문에 클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어진다.
  - 클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못하기 때문에 클라이언트가 누군지 알 수 없다.
  - 그럼 모든 요청에 사용자 정보를 넣어야한다. 하지만, 이렇게하면 보안에 문제도 있고 브라우저를 완전히 종료하면 역시 똑같은 문제가 생긴다.
 
### 쿠키의 이용  
쿠키를 이용하는 예제를 알아보자  
  <image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/5b99702f-67a0-4e6b-9ddc-ac9491385f69">  
  
  - 웹 브라우저에서 로그인 시 사용자 정보를 보내면, 서버에서는 로그인이 성공했을 때 해당 정보를 "쿠키 헤더"에 담아서 응답을 한다.
  - 웹 브라우져 내부에는 쿠키 저장소가 있는데 그 저장소에다가 user=홍길동을 저장해둔다.
 
  <image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/3c4b3571-643e-4aee-a91a-3ede3afb718b">  
    
  - 이제 로그인 이후에 welcome 페이지에 들어간다면, 자동으로 웹 브라우져는 서버에 요청을 보낼 때마다 쿠키 저장소에서 해당 쿠키 값을 꺼내서 요청 메세지에 쿠키를 넣어준다.
  - 서버는 쿠키를 열어보고, 유저가 누구인지 알 수 있다.

그런데 모든 곳에 다 쿠키를 보내면 보안상 문제가 생기고 여러 잠재적인 문제들이 생길 수 있다.  

### 쿠키의 단점  
쿠키 정보는 항상 서버에 전송되기 때문에 아래와 같은 단점이 있다.  
* 네트워크 트래픽 유발
* 보안상 문제 
  - 개인정보 노출에 관련된 문제
  - 사용자의 장치에 저장되는 쿠키의 특성상 사용자의 관리 부실로 인해 쿠키를 탈취 당하거나, 쿠키 정보를 조작하여 다른 사용자로 위장하거나 세션을 도용하는 등
 
** 쿠키를 서버에 보내지 않고 웹 브라우저 내부에 저장하고 필요할 때만 자바스크립트를 통해 사용하고 싶다면 webStorage(localStorage, sessionStorage) 사용  
** 쿠키에는 민감한 정보는 절대 저장해서는 안된다 !!  

### 쿠키의 생명주기  
* Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
  - 만료일이 되면 쿠키 삭제
* 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
* 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

### 쿠키의 도메인 지정  
* 예) domain=example.org
* 도메인을 명시 했을 때는 명시한문서기준도메인과 서브도메인 모두 쿠키에 접근이 가능하다.
  - domain=example.org를 지정해서 쿠키 생성
  - example.org는 물론이고, dev.example.org도 쿠키 접근
* 도메인을 생략 했을 때는 기준도메인만 쿠키에 접근이 가능하다.
  - example.org 에서 쿠키를 생성하고 domain 지정을 생략  
  - example.org 에서만 쿠키 접근가능 dev.example.org는 쿠키 접근 불가능

### 쿠키 경로 설정  
* 예) path=/home
* 경로를 지정했을 경우 경로를 포함한 하위경로페이지만 쿠키 접근가능
* 일반적으로 path=/ 루트로 지정

### 쿠키의 보안  
* 원래 쿠키는 http, https를 구분하지 않고 전송하는데 Secure를 적용하면 https인 경우에만 전송
* HttpOnly를 적용하면 자바스크립트에서 접근 불가(XXS 공격 방지)
* SameSite를 적용하면 요청 도메인과 쿠키에 설정된 도메인이 같은경우만 쿠키 전송 (XSRF 공격 방지)
---


<br>
<br>
<br>
<br>

# 섹션 8
HTTP 헤더 - 캐시와 조건부 요청

<br>

---
## 캐시 기본 동작  
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/262314ba-abb2-4adf-8731-14c2bb150a35">  

```
웹브라우저에 사진을 요청하면 위의 그림처럼 요청한 사진에 대한 데이터가 담긴 HTTP 헤더, HTTP 바디 부분이 응답된다.
캐시가 없다면 동일한 재요청에 대해 HTTP헤더, HTTP바디를 만들어서 다시 응답해준다.
```
데이터 변경되지 않은 동일한 요청이지만 네트워크를 통해 요청을 받아야한다.  
해당 페이지에 이런 사진요청이 많다면 브라우저는 로딩 속도가 느려지기 때문에 사용자는 경험이 좋지 않을 것 이다.  

<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/85260d7f-f604-4dc6-99c8-9fb92fd3bb44">  

```
1. 서버에서 캐시를 적용하면 응답 헤더에 cache-control이라는 것을 넣어줄 수 있다. (캐시가 유효한 시간을 설정한 것)
2. 클라이언트는 브라우저의 캐시에 응답결과를 저장한다.
3. 그리고 다음에 요청을 했을 때 브라우저는 캐시를 탐색하고 유효한 것이 있다면 네트워크를 통신하지 않고 데이터를 반환한다.
4. 만약 캐시 유효 시간이 지나면 다시 서버에 요청을해서 데이터를 받고 캐시를 덮어 씌운다.
```

## 검증 헤더와 조건부 요청
캐시 시간이 초과됐을 때는 무조건 서버로 요청을 보내서 응답을 받아야한다.  
하지만, 서버의 데이터와 클라이언트의 데이터에 변화가 없고 단순히 캐시 유효 시간이 초과된거라면 그 때마다 소모되는 비용이 너무 아깝게 된다.  
이러한 점을 개선하기 위한 방법을 알아보자.  

### 검증 헤더  
* 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
* Last-Modified , ETag  
  
### Last-Modified  

<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/3cbe5656-6f14-4634-baa2-2ce89e28aa37">  
  
```
위의 그림과 같이 최종 수정된 시간(Last-Modified)를 응답 헤더에 넣어둔다.
그럼 이전과 다르게 캐시에 Last-Modified 정보를 같이 저장한다.
```
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/9710f6d5-c001-47c3-9bf0-6f0c933c7c27">  
  
<image style="width: 600px" src="https://github.com/Kimpossible94/TIL/assets/80395024/99cbfc0b-3e60-4d02-a7b3-4172f2a3cdee">  

```
그리고 캐시 유효 기간이 만료되었다면 if-modified-since라는 헤더 속성을 통해 캐시가 가지고있는 최종 수정일 값을 넘긴다.
그럼 서버에서는 최종 수정일을 비교해서 수정이 되지 않았다면 304 Not Modified 라는 응답을 보낸다.
* 이 때는 HTTP 바디가 없다.
응답을 받고 변화가 없다는 것을 알았기 때문에 캐시 유효 기간만 다시 갱신한다.

네트워크를 사용하지만 HTTP 바디를 다시 받지않고 유효기간만 갱신하면 되기 때문에 전송 용량을 줄여 비용을 절감할 수 있다.
```

**Last-Modified 단점**  
날짜로만 비교하기 때문에 a에서 b로 다시 b에서 a로 변경했을 경우에도 똑같이 a 상태이지만 다시 데이터를 보내야한다.  
그리고 서버에서 별도의 캐시 로직을 관리하고 싶은 경우에는 사용할 수 없다. (스페이스나 주석처럼 크게 영향이 없는 경우에는 캐시를 유지하게 하고 싶은 경우)

### ETag  
캐시용 데이터에 임의의 고유한 버전을 담아주는 것을 말한다. (ETag: "v1.0", ETag: "a2jiodwjekjl3")  
만약 데이터가 바뀌었다면 이 이름을 바꾸어서 변경함 (Hash를 다시 생성)  
클라이언트 입장에서는 ETag를 보내서 같으면 유지, 다르다면 다시 받으면 된다.


### 조건부 요청 헤더  
* 검증헤더로 조건에 따른 분기
* If-Modified-Since: Last-Modified 사용
* If-None-Match: ETag 사용
* 조건이 만족하면 200 OK
* 조건이 만족하지 않으면 304 Not Modified

## 캐시 제어 헤더  
* Cache-Control: 캐시 제어  
  - Cache-Control: max-age (캐시 유효 시간, 초 단위)  
  - Cache-Control: no-cache (데이터를 캐시해도 되지만, 캐시를 항상 원(origin)서버에 검증하고 사용해라.)  
                            (중간 캐시 서버가 있을 수 있기 때문에 원서버에 검증을 해야함.)  
  - Cache-Control: no-store (데이터에 민감한 정보가 있으므로 저장하면 안됨)  
* Pragma: 캐시 제어(하위 호환)  
* Expires: 캐시 유효 기간(하위 호환)  
  - 캐시 만료일을 정확한 날짜로 지정  
  - 지금은 더 유연한 Cache-Control: max-age 권장
  - Cache-Control: max-age와 함께 사용하면 Expires는 무시
 
## 프록시 캐시  
우리나라에서 미국에 있는 원서버에 접근하려면 네트워크가 아무리 빨라도 같은 지역보다 응답에 시간이 걸릴 수 밖에 없다.  
그래서 같은 나라의 어딘가에 프록시 캐시 서버를 도입해놓고 프록시 캐시서버에 접근하도록 만든다.  

<img width="600px" alt="image" src="https://github.com/Kimpossible94/TIL/assets/80395024/d68b1ac4-150b-4fce-a433-a5a25305f53f">  

```
위의 그림처럼 원서버에 직접 통신하는게 아니라 프록시 캐시 서버와 통신하기 때문에 원서버에 접근하지 않아도 되어서 응답을 빠르게 받을 수 있다.
```

## 캐시 무효화  
캐시를 적용안해도 브라우저가 임의로 캐시를 하는 경우가 있다 이것을 방지하기위해 캐시 제어 헤더에 확실하게 캐시를 무효화 할 수 있는 속성이 있다.  
해당하는 경우에는 
Cache-Control: no-cache, no-store, must-revalidate
그리고 하위 호환을 위해 Pragma: no-cache 이렇게 넣어주면 된다.  

* Cache-Control: no-cache
  - 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용(이름에 주의!)
* Cache-Control: no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨  (메모리에서 사용하고 최대한 빨리 삭제)
* Cache-Control: must-revalidate
  - 캐시 만료후 최초 조회시 원 서버에 검증해야함
  - 원 서버 접근 실패시 반드시 오류가 발생해야함 - 504(Gateway Timeout)
  - must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
* Pragma: no-cache (HTTP 1.0 하위 호환)

### no-cache와 must-revalidate의 비교  
no-cache를 사용하면 항상 원서버에 검증하는데 must-revalidate는 왜 필요할까 ?  

<img width="600" alt="image" src="https://github.com/Kimpossible94/TIL/assets/80395024/495491e3-83c1-4f66-9dc1-54dcb1e0a9f9">  

```
no-cache의 경우 그림처럼 요청을 받은 프록시 서버가 no-cache이므로 원서버로 요청을 위임한다.
그리고 원서버에 문제가 있는 경우 no-cache에서는 에러 또는 예전에 있던 데이터라도 보여주며 200 OK를 보낸다.
하지만 통장 잔고같은 경우 과거 데이터를 보내거나하면 안된다.
이럴 경우 확실하게 에러를 보내는 must-revalidate를 사용한다.
```

<img width="600" alt="image" src="https://github.com/Kimpossible94/TIL/assets/80395024/e0a22055-6895-4e92-9b3a-3c98c8ea0e42">  
```
must-revalidate는 원서버에서 검증할 수 없는 경우 무조건 504 에러를 발생하도록 되어있다.
```

---
