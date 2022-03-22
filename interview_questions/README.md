# Interview Questions

실제로 받았던 면접 질문들 정리

- button, a tag 로 감싸는데 접근성이 저하된다..
    - [https://stackoverflow.com/questions/6393827/can-i-nest-a-button-element-inside-an-a-using-html5](https://stackoverflow.com/questions/6393827/can-i-nest-a-button-element-inside-an-a-using-html5)
    - a tag로 button을 감싸면 안됨
    - If you are trying to have a button that links to somewhere, wrap that button inside a `<form>` tag as such
        
        ```jsx
        <form style="display: inline" action="http://example.com/" method="get">
          <button>Visit Website</button>
        </form>
        ```
        
- CSS outline 단축속성
    - 모든 외곽선 속성을 설정
    - outline-color, outline-style, outline-width
- CSS Box-model MARGIN, PADDING
    - margin: 바깥쪽 여백
    - padding: 안쪽 여백
- 화살표 함수, 기본 함수의 차이
    - 화살표 함수 - ES6
        - this 바인딩이 없음.
        - 화살표 함수를 호출한 바깥쪽 스코프의 this가 됨
        - this의 스코프를 바꾸지 않을 때 유용하게 사용.
- 이벤트 버블링, 캡쳐링
    - 버블링: 상위 노드(부모)로 전파
    - 캡쳐링: 상위 노드에서 이벤트 근원지로 이벤트를 전파
    - `target.addEventListener(type, listener, useCapture);`
        - `useCapture` 인자
            - default: false
            - false: bubbling
            - true: capturing
- `React.setState()` 이 비동기인 이유
    - [https://ko.reactjs.org/docs/faq-state.html](https://ko.reactjs.org/docs/faq-state.html)
    - 단점: 동기적으로 `state` 가  업데이트 되지 않아 불편함
    - 장점: 비동기이므로 효율적인 렌더링이 가능
- `React.useCallback(() => {}, [])`, `React.useEffect(() => {}, [])`
    - 얕은 비교
    - [https://stackoverflow.com/questions/54095994/react-useeffect-comparing-objects](https://stackoverflow.com/questions/54095994/react-useeffect-comparing-objects)
- 메모이제이션
    - `useRef`, `createRef`
    - 
    
- Browser Rendering - Before Rendering
    - 크롬 애플리케이션에 구현된 Windows Message Loop에서 WM_KEYUP 메시지를 처리합니다. 크롬 애플리케이션에 해당 메시지가 들어왔을 때 연결된 이벤트 리스너가 실행될 것입니다. 해당 이벤트 리스너는 [http://google.com](http://google.com/) 으로 저장되어 있는 쿠키와 함께 HTTP Request를 만들고,
    - [http://google.com의](http://google.xn--com-yh0o/) IP주소를 알아내기 위해 함수를 호출할 것입니다. 크롬이 libdns을 사용한다고 가정했을 때, libdns는 UDP socket을 만들고, 커널을 호출합니다. 커널은 설정된 UDP Stack을 통해 하드웨어가 UDP 패킷을 보내도록 합니다.
    - [http://google.com의](http://google.xn--com-yh0o/) IP 주소를 질의하기 위해 컴퓨터는 루트 DNS에 .com 네임서버 주소를 질의하게 됩니다. 루트 DNS는 .com 네임서버의 IP주소를 응답하여 보내고, 다시 컴퓨터는 이를 확인하여 UDP socket을 통해 .com 네임서버에 [http://google.com의](http://google.xn--com-yh0o/) 서버 주소를 질의하게 됩니다.
    - 물론 이 과정은 필수적인 과정은 아닙니다. 왜냐하면 유저는 대부분 DNS 캐시 서버 (예를들어, 1.1.1.1, 8.8.8.8, 또는 ISP에서 제공하는 서버)에 이미 [http://google.com의](http://google.xn--com-yh0o/) DNS 레코드가 캐시되어 있을 것이므로 캐시 서버로 DNS 질의 패킷을 보내게 되면 루트 DNS 서버에 질의하는 과정을 생략할 수 있을 것입니다.
    - 이제 크롬 소프트웨어는 [http://google.com의](http://google.xn--com-yh0o/) IP주소를 얻었습니다. [http://google.com은](http://google.xn--com-7e0o/) HSTS Preload되어있으므로 TCP 프로토콜로 443포트로 연결을 시도할 겁니다. 그리고 ClientHello 를 보낼 것입니다.
    - ClientHello에는 Client가 지원하는 Cipher Suite, SNI 등등이 들어가 있습니다. 이를 받은 서버는 Server Hello 와 함께 Certificate를 전달합니다. 이후에는 협의된 Cipher Suite에 따라 암호화가 진행됩니다.
    - 클라이언트는 이후 HTTP 요청을 암호화해서 보내게 되고, 구글 서버는 HTTP 응답을 암호화해서 보내게 됩니다
