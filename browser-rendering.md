## 브라우저 렌더링

정확하게는 브라우저의 주소창에 google.com을 치면 일어나는 일들

### 1. Browser UI

URL 치기

### 2. Browser Engine

크롬의 경우 Windows Message Loop에서 WM_KEYUP 메시지를 처리.

크롬 애플리케이션의 이벤트 리스너가 실행

google.com에 저장된 쿠키가 있다면 쿠키와 함께 HTTP Request를 만들고 google.com의 IP주소를 알아내기 위하여 특정 함수를 호출

### 3. Connect with DNS Server 

TL;DR
Root DNS -> .com DNS -> google.com (캐시 서버 관여)
-> HSTS Preload, TCP 443 Port -> Client Hello/Server Hello -> Https Request/Response

크롬이 사용하는 함수가 libdns이라고 가정하면 libdns는 UDP socket을 만들고, 커널을 호출한다. 커널은 설정된 UDP Stack을 통해 하드웨어가 UDP 패킷을 보내도록 한다.

IP 주소를 물어보기 위해 Root DNS에 .com 네임서버 주소를 질의하고 DNS가 네임서버의 IP 주소를 응답

컴퓨터가 이를 확인 후 .com 네임서버에 google.com 서버주소를 질의하고 google.com의 IP주소를 크롬이 얻음.

유저가 대부분 캐시 서버(1.1.1.1, 8.8.8.8, ISP 제공 서버 등 )에 이미 google.com의 DNS 레코드가 캐시되어있을 것이다. 캐시서버로 DNS 질의 패킷을 보내면 루트 DNS 서버에 질의 과정은 생략 가능.


google.com은 HTTP Strict-Transport-Security response header (종종 HSTS (en-US) 로 약칭) Preload 되어있으므로 TCP 프로토콜로 443포트에 연결을 시도할 것,
이후는 ClientHello -> Client Cipher Suite, SNI, etc -> 서버는 ServerHello와 Certificate를 전달. 

이후 협의된 Cipher Suite에 따라 암호화가 진행.

클라이언트가 HTTP 요청을 암호화해서 보내고, 구글 서버는 HTTP 응답을 암호화해서 보냄


### Browser Rendering Engine
  * FireFox : Mozilla's  Gecko Engine 
  * Safari, Chrome: Webkit Engine



#### HTML/CSS 파싱

브라우저의 렌더링 엔진이 통신으로 받은 문서의 내용을 얻음. 보통 8KB 단위로 전송. 그렇게 얻은 HTML/스타일 문서를 파싱
-> DOM 트리를 구축한다.
-> link tag -> html 파싱 중지, 외부 CSS 파일을 포함한 스타일 요소도 파싱.
-> css 파싱이 끝나면 html 파싱 시작, DOM 트리 구축, 완성.
-> 스타일 요소를 파싱한 정보와 DOM 트리 합쳐서 렌더 트리를 구축

렌더 트리 : 시각적 속성 (예. 색, 면적)이 있는 사각형을 포함하며 정해진 순서대로 화면에 표시됨.

#### 렌더 트리 배치
노드가 정확한 위치에 표시됨 (margin, padding, position 등의 요소겠지?)


#### 렌더 트리 그리기
UI 백엔드에서 렌더 트리의 노드들을 가로지르며 형상을 만들어내기.

#### 총괄 정리

이 모든 과정은 점진적인데, UX를 위해 렌더링 엔진이 모든 HTML을 파싱하는 것을 기다리지 않고, 렌더 트리 배치 및 그리기 과정을 시작한다. 이 과정은 웹킷과 게코 엔진의 동작과정이 다르지만, 동작 과정은 기본적으로 동일.

#### DOM 트리와 렌더 트리
1:1 관계가 아니지만, 렌더러는 DOM 요소에 부합함.
* ex) selector같은 경우 여러 개의 DOM이 필요
* ex) head, display: none -> dom에 안보임
* exex) visibility: hidden -> dom에 보임

### 글쓴이의 생각

네이버 D2 블로그 글을 꼼꼼하게 읽어보도록 하자.
렌더링 엔진의 파싱 과정에서 DOM 트리 파싱까지 알고리즘이랑 HTML/CSS 파싱 등등.... 정규표현식도 사용하는 등의 일련의 과정이 있음. 

Naver D2 Blog의 브라우저 관련 내용은 주로 브라우저의 렌더링에 초점이 맞춰져있으며 브라우저의 UI에서 브라우저 엔진에 관한 내용은 자세히 표기되어있지 않는 것 같다. 

참고자료
[Naver D2 Blog](https://d2.naver.com/helloworld/59361)
[Google Cloud Blog](https://cloud.google.com/blog/topics/inside-google-cloud/google-cloud-support-engineer-solves-a-tough-dns-case)
