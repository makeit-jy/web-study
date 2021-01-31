# 9 HTTP 헤더

- 헤더란
    - 헤더는 메시지의 바디에 대한 부가적인 정보, 즉 메타 데이터를 표현한다
    - 클라이언트와 서버는 헤더를 보고 메시지에 대한 동작을 결정한다
    - 인증과 캐시 사용도 헤더로 실현
    - 전자메일 메시지 헤더와 유사한 점이 많다
- 구성 살펴보기
    - Date

        값으로 날짜와 시간을 가지는 헤더

        ```java
        Date: Tue. 06 Jul 2010 03:21:05 GMT
        ```

    - Content-Type

        그 메시지의 바디 내용이 어떠한 종류인가를 미디어 타입으로 나타냄

        ```java
        Content-Type: application/xhtml +xm
        Content-Type: video/mp4
        ```

    - charset

        미디어 타입이 가지는 파라미터로 문자 인코딩을 지정한다

        ```java
        Content-Type: application/xml; charset=utf-8
        ```

    - Content-Language

        언어 태그. 언어코드-지역코드

        ```java
        Content- Language: ko-KR
        ```

    - Accept

        클라이언트와 서버가 어떤 미디어 타입과 문자 인코딩, 언어 태그를 사용할지 교섭하여 정하는 Content Negotiation

        ```java
        Accept: text/ html, application/xhtml+xml, application/xml; q=O.9, */*;q=0.8
        ```

        Accept-Charset, Accept-Language

    - Content-Length

        미리 사이즈를 알고 있는 리소스인 정적 파일 등을 전송할때 사용

    - Transfer-Encoding

        쪼개서 보낸다

        동적 파일의 응답성능 저하를 막기위한 방법으로 Transfer-Encoding : chunked 를 지정하면 사이즈를 모르는 바디를 조금씩 전송할 수 있다

        ```java
        POST /test HTTP/ l.l
        Host: example.com
        Transfer-Encoding: chunked
        Content-Type: Text/ plain; charset=utf-8
        10
        The brow fox ju
        10
        mps quickly over
        e
        the lazydog
        0
        (여기에도 빈 줄
        ```

    - Authorization

        인증

        ```java
        DELETE /test HTTP/ l.l
        Host: example.com
        Authorization: Basc dXNlcjpwYXNzd29yZA==
        ```

        Basic , Digest(복잡,보안up) , WSSE

    - Cache-Control
        - Pragma : 캐시 사용 안한다
        - Expires : 캐시의 유효기한을 나타낸다
        - Cache-Control : 둘 합치고 더 복잡한 내용 구현(max-age)
    - If-Modified-Since
        - 서버의 리소스가 이 이후로 변경되지 않았다면 리다이렉션 상태코드를 반환한다(Last-Modified)
        - If-None-Match - Etag(엔티티 태그) 를 이용해 서버상의 리소스가 변경되어 있지 않으면 304 Not Modified
    - Keep-Alive

        HTTP1.0 에서 TCP 커넥션을 절단하지 않고 계속 접속을 유지하여 동작을 빠르게 하는 방법

        HTTP1.1 에서는 기본으로 작동

        응답을 기다리지 않고 같은 서버에 요청을 송신할 수 있다(파이프라인화)

        Connection : close 를 통해 끊을 수 있음