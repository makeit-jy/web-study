# REST - 웹 아키텍쳐 스타일

### **웹의 표준화**

- Why?: 동시다발적으로 보급되는 웹, 이러한 상황속에서 정해진 표준이 없었음
- What?: HTTP & URI & HTML에 대한 표준화가 요구됨
    - 각 회사의 서버, 클라이언트 사이에서 이용되면서 동시에 상호 운용성이 요구되었기 때문
- How?: W3C (Word Wide Web Consortium) 설립 at 1994
    - 표준화 작업 for **HTML**, XML, HTTP, URI, **CSS**

### **REST (Representational State Transfer) 탄생**

- 기존 웹의 protocols와 기술을 쓰는 Stateless Arichitecture
- HTTP 1.0과 1.1의 제정자중 한명인 Roy Field (PhD in UCI)에 의해 2000년에 논문으로 제출

### **REST vs SOAP**

- SOAP
    - HTTP, HTTPS, SMTP 등을 통해 XML 기반의 메시지를 네트워크 상에서 교환하는 protocol
    - But SOAP는 메시지 전송 방법만을 규정한 스펙 → 실제로 시스템을 구축할 때는 SOAP 상에 서비스 별로 protocol 정의 필요 → 각 벤더마다 정의하게 되면 표준화가 다시 필요해짐

[REST vs SOAP](https://www.notion.so/12ec76c976c74f38854a7ce9fe37e11d)

- ([https://www.guru99.com/comparison-between-web-services.html](https://www.guru99.com/comparison-between-web-services.html))

### **REST**

- 웹의 아키텍처 스타일 (= 웹의 (매크로) 아키텍처 패턴)
    - 복수의 아키텍처의 공통된 성질, 양식, 규정 혹은 독특한 방식을 가리킴
    - 시스템의 아키텍처를 결정할 때 나침반이 되는 역할
    - 디테일하게는 클라이언트 서버 구조에서 파생된 아키텍처 스타일 순수한 클라이언트/서버 아키텍처 스타일에 몇 가지 제약을 더해가면 REST 아키텍처 스타일이 됨
- (아키텍처 스타일에는) MVC (Model-View-Controller), Pipe and Filter, Event System 등이 있음
- 아키텍처와 아키텍처 스타일은 별개 (디자인과 디자인 패턴이 다르듯이)

[제목 없음](https://www.notion.so/bd2fd5cd19d04ac79ed2ab3c8173a398)

- **리소스 (Resource)**
    - 웹상에 존재하는 이름을 가진 모든 정보 (추상적인 개념)
    - 전 세계의 무수한 리소스는 각각 URI로 의미있는 이름을 가짐
    - 예시
        - 서울의 일기예보
            - https://weather.naver.com/rgn/ccityWetrWarea.nhn?cityRgnCd=CT00100058
        - Dijkstra의 논문 "Go To Statement Considered Harmful"
            - http://www.ecn.purdue.edu/ParaMount/papers/dijkstra68goto.pdf
    - → 리소스의 이름이란 URI를 뜻함
        - URI로 식별할 수 있음
    - URI를 이용함으로써, 프로그램은 리소스가 표현하는 정보에 접근할 수 있다.
        - 어드레스 가능성 (Addressability)
            - URI가 지니고 있는 리소스를 간단히 가리킬 수 있는 성질을 가리킴
    - 1개의 리소스는 복수의 URI를 가질수 있음
        - 예시
            - http ://weather.example.com/seoul/today
            - http ://weather.example.com/seoul/2011-01-01
    - Resource Representation
        - 서버와 클라이언트 사이에 주고받는 어떤 구체적인 데이터

    ---

    ### 아키텍처 스타일

    - *클라이언트/서버 (Client Server)*
        - 웹
            - HTTP라는 protocol을 이용해 클라이언트와 서버가 서로 통신하는 클라이언트/서버의 아키텍처 스타일을 채용

            ![REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled.png](REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled.png)

            - 클라이언트가 서버에 request를 보내면 서버가 클라이언트에 response를 돌려줌
        - 단일 컴퓨터 상에서 모든것을 처리하는것이 아니기 때문에 클라이언트와 서버로 분리해서 처리 가능
            - → 클라이언트를 멀티플랫폼으로 구성 가능
        - 복수의 서버를 조합해 확장함으로써 가용성을 올릴 수 있음
            - ∵ 서버는 데이터 스토리지로서 기능만을 제공하면 됨
            - ∵ UI는 클라이언트에서 담당

    - *스테이트리스/서버 (Stateless Server)*
        - 스테이트리스
            - "클라이언트의 애플리케이션 상태를 서버에서 관리하지 않는다" 를 의미

        ![REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled%201.png](REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled%201.png)

        - 서버 측의 구현을 간략화 할 수 있음
            - ∴ 서버는 클라이언트로부터 요청에 응답한 뒤 바로 서버의 자원을 해제할 수 있음

    - *캐시*
        - 리소스의 신선도에 기초해, 한번 가져온 리소스를 클라이언트 쪽에서 돌려쓰는 방식

        ![REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled%202.png](REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled%202.png)

        - 서버와 클라이언트의 사이의 통신량을 줄여 네트워크 대역의 이용과 처리시간을 축소하여 효율적으로 처리 가능
        - but 오래된 캐시를 이용해 정보의 신뢰성이 떨어질 수 있음

    - *유니폼 인터페이스 (Uniform Interface)*
        - URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일

        ![REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled%203.png](REST%20-%20%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A7%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%20d1cff1c9876b46338e3048f645a53db3/Untitled%203.png)

        - 인터페이스의 유연성에 제약을 가함으로써 전체적인 아키텍처가 간결해질수 있고 인터페이스를 통일함으로써 클라이언트와 서버 구현의 중립성이 향상됨

    - *계층화 시스템*
        - 시스템을 몇 개의 계층으로 분리하는 아키첵처 스타일
        - 시스템 전체를 계층화하기 쉬움

    - *코드 온 디맨드*
        - 프로그램 코드를 서버에서 다운받아 클라이언트에서 실행하는 아키텍처 스타일
        - 예시
            - JavaScript
            - Java 애플릿
            - Flash

    [제목 없음](https://www.notion.so/9f1b7d57eef04296a5b3055a2e48b28c)
