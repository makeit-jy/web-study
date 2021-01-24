# Chapter11 microformats

HTML은 표제나 단락 등의 구조를 정의한 범용 문서포맷입니다.
microformats를 이용하면 링크의 상세한 의미와 이벤트 정보를 표현할 수 있습니다.

[시맨틱 웹 정리](https://www.notion.so/22d09ff39c074d4caafd02fca1b6c2a1)

# 01 심플한 시맨틱 웹

시맨틱 웹이란?
웹에 존재하는 수많은 웹페이지들에 메타데이터를 부여하여 기존의 잡다한 데이터 집합이었던 웹페이지를 '의미'와 '관련성'을 가지는 거대한 데이터베이스로 구축하고자 하는 발상이다.
[https://ko.wikipedia.org/wiki/시맨틱_웹](https://ko.wikipedia.org/wiki/%EC%8B%9C%EB%A7%A8%ED%8B%B1_%EC%9B%B9)
[https://poiemaweb.com/html5-semantic-web](https://poiemaweb.com/html5-semantic-web)

- 예시

```html
//동일한 외형을 갖는다.
<font size="6"><b>Hello</b></font>    //non-semantic 요소
<h1>Hello</h1>                        //semantic 요소 -> 제목
```

- HTML5에서 새롭게 추가된 시맨틱 태그

시맨틱 태그란 브라우저, 검색엔진, 개발자 모두에게 콘텐츠의 의미를 명확히 설명하는 역할을 한다.

![Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled.png](Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled.png)

SOAP 기반의 웹 API
RDF(Resource Description Framework)

vs

RESTful한 웹 API
microformats

# 02 시맨틱스(의미론)란

### 프로그래밍 언어에서의 의미론

프로그래밍 언어가 가진 의미를 확정시키기 위한 이론

- 컴파일러, 언어의 문법을 해석하여 기계어로 번역하는 작업
- 언어의 스펙에 따른 문법을 형식적으로 기술

### 웹에 있어서의 의미론

리소스가 가진 의미를 확정시키기 위한 이론

- 웹 리소스의 의미를 사람과 프로그램 모두 읽고 해석할 수 있게!
- 결국 사람이 읽고 이해하는 웹페이지의 의미를 프로그램도 처리할 수 있도록 형식적으로 의미를 기재하기 위한 기술이 시맨틱 웹

# 03 RDF와 microformats

### RDF

'트리플' : 주어, 술어, 목적어

```html
<rdf:RDF xmlns:rdf="http://...">
  <rdf:Description rdf:about="http://...">
    <cc:license xmlns:cc="http://..."/>
	</rdf:Description>
</rdf:RDF>
```

- 문제점
    1. 작성이 복잡
    2. 통일적인 작성 X
    3. 대상 데이터와는 독립된 메타 데이터 필요

### microformats

- RDF의 문제점 해소

```html
<html xmls="http://...">
	...
	<body>
		...
		<p>
			이 웹페이지의 권리는
			<a rel="license" href="http://...">Creative Commons by-sa 3.0</a>
			에 따릅니다.
		</p>
	</body>
</html>
```

# 04 microformats의 표준화

[http://microformats.org/wiki/Main_Page-ko](http://microformats.org/wiki/Main_Page-ko)

![Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled%201.png](Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled%201.png)

![Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled%202.png](Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled%202.png)

# 05 microformats의 분류

### 단순(elemental) microformats

rel-license와 같이 링크관계를 사용해 메타 데이터를 표현하는 포맷

1. rel-license : 라이선스 정보

    ```html
    이 웹페이지의 권리는
    <a rel="license" href="http://cre...">Creative Commons by-sa 3.0</a>
    에 따릅니다.
    ```

2. rel-nofollow : 스팸 링크 방지

    ```html
    스팸 사이트
    <a href="http://spam.example.com" rel="nofollow">http"//spam.example.com</a>
    ```

### 복합(compound) microformats

hCalendar와 같이 주로 class 속성을 사용해 계층구조가 있는 메타 데이터를 표현하는 포맷

1. hCalendar : 이벤트 정보

    ```html
    <ul class="vevent"> // class속성값이 vevent인 ul 요소는 하나의 이벤트 정보를 표현
    	<li class="summary">
    		<a class="url" href="http://hahahoho.kr/..">
    			[웹을 지탱하는 기술] chapter11 microformats
    		</a>
    	</li>
    	<li>일시 : 2021년 1월 20일
    		<abbr class="dtstart" title="2021-01-20T22:00:00+09:00">22:00</abbr>~
    		<abbr class="dtend" title="2021-01-20T23:00:00+09:00">23:00</abbr>
    	</li>
    	<li>
    		<span class="location">울집</span>에서
    	</li>
    </ul>
    ```

2. hAtom : 갱신정보

    ```html
    <div class="hfeed">
    	<div class="hentry">
    		<h2 class="entry-title">
    			<a href="http://blog.example.com/20210120/study" rel="bookmark">
    				hAtom의 테스트
    			</a>
    		</h2>
    		<div class="entry-content">
    			<p>hAtom을 테스트</p>	
    		</div>
    		<p><abbr class="updated" title="2021-01-20T22:25:00+09:00">
    			2021년 1월 20일 22:25
    		</abbr></p>
    	</div>
    	...
    </div>
    ```

![Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled%203.png](Chapter11%20microformats%200c9d7e74f34446e292d3f16367419526/Untitled%203.png)

# 06 microformats와 RDFa

### microformats의 문제점

class, rel속성의 중복으로 인한 오판 및 생성 제약

### RDFa에서의 해결과 남은 문제점

```html
이 웹페이지의 권리는
<a xmlns:cc="http:cre..." rel="cc:license" href="http://cre...">
Creative Commons by-sa 3.0</a>에 따릅니다.
```

xmlns:cc로 이름공간을 정의하였으나 복잡해졌다.

# 07 microformats의 가능성

# 08 리소스 표현으로서의 microformats

- 프로그램을 위해 별도의 웹  API를 제공하는 스타일의 문제점
(프로그램용 XML, JSON 데이터 구조 이용)
1. 웹 서비스와 웹 API에서 제공하는 기능이 달라지기 쉽다.
2. 개발 규모의 증대에 따른 유지 보수성 저하
3. 웹 API에 필요한 기술의 습득 비용

- microformats을 이용하여, 기존의 웹페이지를 그대로 웹 API로 제공함으로써
위 3가지 문제점을 줄일 수 있다.
1. 양쪽의 기능차 X
2. 기존의 웹페이지에 미치는 영향 적음
3. 개발 비용 낮음