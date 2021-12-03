# 타임리프 기본 문법
## 타임리프 특징
- 서버 사이드 HTML 렌더링
- 네츄럴 템플릿
  - 타임리프는 순수 HTML을 유지하기 때문에 웹 브라우저에서 파일을 직접 열어도 내용을 확인할 수 있고, 서버를 통해 뷰 템플릿을 거치면 동적으로 변경된 결과를 확인할 수 있다.
  - 이렇게 **순수 HTML을 그대로 유지하면서 뷰 템플릿도 사용할 수 있는 타임리프의 특징을 네츄럴 템플릿**(natural templates)이라 한다.
- 스프링 통합 지원
- - -
## 타임리프의 기본 기능
- 타임리프의 사용 선언
<pre>
<code>
 &lt;html xmlns:th="http://www.thymeleaf.org"&gt;
 </code>
</pre>

- 기본 표현식
  -  간단한 표현:
     -  변수 표현식: ${...}
     -  선택 변수 표현식: *{...}
     -  메시지 표현식: #{...}
     -  링크 URL 표현식: @{...}
     -  조각 표현식: ~{...}
  - 리터럴
    - 텍스트: 'one text', 'Another one!',…
    - 숫자: 0, 34, 3.0, 12.3,…
    - 불린: true, false
    - 널: null
    - 리터럴 토큰: one, sometext, main,…
  - 문자 연산:
    - 문자 합치기: +
    - 리터럴 대체: |The name is ${name}|
  - 산술 연산:
    - Binary operators: +, -, *, /, %
    - Minus sign (unary operator): -
  - 불린 연산:
    - Binary operators: and, or
    - Boolean negation (unary operator): !, not
  - 비교와 동등:
    - 비교: >, <, >=, <= (gt, lt, ge, le)
    - 동등 연산: ==, != (eq, ne)
  - 조건 연산:
    - If-then: (if) ? (then)
    - If-then-else: (if) ? (then) : (else)
    - Default: (value) ?: (defaultvalue)
  - 특별한 토큰:
    - No-Operation: _

- - -
## 텍스트 - text, utext

타임리프는 기본적으로 HTML 태그의 속성에 기능을 정의해서 동작한다.
th:text를 사용하면 된다.
```html
<span th:text="${data}">
```

HTML 태그 속성이 아니라 직접 출력할 수도 있다.
```html
[[${data}]]
```

**Escape**

HTML 문서는 <,> 같은 특수 문자를 기반으로 정의된다. 따라서 HTML 화면을 생성할 때 특수 문자를 주의해서 사용해야 한다.

b태그를 사용해서 Spring!을 진하게 표현해보자

- 웹 브라우저 : ```: Hello <b>Spring!</b> ```  
- 소스보기 : ``` Hello &lt;b&gt;Spring!&lt;/b&gt; ```  

소스를 보면 < 부분이 ```&lt;``` 로 변경된 것을 확인할 수 있다.

HTML 엔티티

웹 브라우저는 < 를 태그의 시작으로 인식한다. 따라서 <를 문자로 표현할 수 있는 방법이 필요한데 그것이 HTML 엔티티이다. 
HTML 에서 사용하는 특수 문자를 HTML 엔티티로 변경하는 것을 이스케이프(escape)라고 한다. 

그래서 타임리프는 2가지 기능을 제공한다.
- th:text  : 이스케이프 기능 o
- th:utext : 이스케이프 기능 x
- - -
## 변수 - SpringEL

- **변수 표현식** : ${...}  
  이 변수 표현식에는 스프링 EL 표현식을 사용할 수 있다.

```html
<span th:text="${user.username}"></span>
<span th:text="${users[0].username}"></span>
<span th:text="${userMap['userA'].getUsername()}"></span>
```

타임리프는 스프링 방식을 그대로 사용하기 때문에 여러가지 방법으로 접근해서 데이터를 조회할 수 있다.

- Object
  - user.username :  username을 프로퍼티 접근
  - user['username'] : 위와 같다.
  - user.getUserName() : user의 getUsername()을 직접 호출
- List : 위와 같이 사용 가능하다.
- Map : 위와 같이 사용 가능

**지역 변수 선언**
- ```th:with``` 를 사용하면 지역 변수 선언, 선언한 태그 안에서만 사용 가능하다.
```html
<div th:with="first=${users[0]}">
 <p>처음 사람의 이름은 <span th:text="${first.username}"></span></p>
</div>
```
- - -
## 기본 객체들
- ${#request}
- ${#response}
- ${#session}
- ${#servletContext}
- ${#locale}

### 편의 객체도 제공
- HTTP 요청 파라미터 접근 : param
  - ```${param.paramData}```
- HTTP 세션 접근 : session
  - ```${session.sessionData}```
- 스프링 빈 접근 : @ : 빈에 접근해서 해당 빈의 메서드를 실행시킬 수 있다.
  - ```${@helloBean.hello('Spring!')}```

※ 빈을 사용하는 경우는 먼저 컨트롤러에서 처리해서 화면에 넘기고, 그게 반복되는 작업일 때 사용하는게 좋다.
- - -
## URL 링크
- 타임리프에서 URL을 생성할 때는 ```@{...}``` 문법을 사용하면 된다.

**단순한 URL**
- ```@{/hello} -> /hello```

**쿼리 파라미터, 경로 변수 처리**
- ```@{/hello/{param1}(param1=${param1}, param2=${param2})}```
  - --> ```/hello/data1?param2=data2```
  - ()에 있는 부분은 쿼리 파라미터로 처리된다.
  - URL 경로상에 변수가 있으면 ()부분은 경로 변수로 처리된다.

- - -
## 리터럴(Literals)
- 타임리프에서 문자 리터럴은 항상 '(작은 따옴표)로 감싸야 한다.
- 하지만 공백 없이 쭉 이어진다면 하나의 의미있는 토큰으로 인지해서 작은 따옴표를 생략할 수 있다.

**오류**
- ```<span th:text="hello world!"></span>``` 오류 발생
- 공백이 있다면 ' '로 감싸야한다.

- - -
## 연산
- 자바와 크게 다르지 않다. HTML 엔티티만 주의하자
- 비교연산: HTML 엔티티를 사용해야 하는 부분을 주의하자
  - ```> (gt), < (lt), >= (ge), <= (le), ! (not), == (eq), != (neq, ne)```
- 조건식: 자바의 조건식과 유사하다.
  - ```<span th:text="(10 % 2 == 0)? '짝수':'홀수'"></span>```
- Elvis 연산자: 조건식의 편의 버전
  - ```<span th:text="${data}?: '데이터가없습니다.'"></span>```
- No-Operation: _ 인 경우 마치 타임리프가 실행되지 않는 것 처럼 동작한다. 이것을 잘 사용하면 HTML
의 내용 그대로 활용할 수 있다. 마지막 예를 보면 데이터가 없습니다. 부분이 그대로 출력된다
  - ``` <span th:text="${nullData}?: _">데이터가없습니다.</span> ```
  - 여기서 nullData = null 이므로 기존의 text가 출력된다.
- - -
## 속성 값 설정(Attribute)

**속성 설정**
- ```th::*``` : 속성을 지정하면 타임리프는 지정한 속성으로 대체한다. 기존 속성이 없다면 새로 만든다.

**속성 추가**
- ```th:attrappend``` : 속성 값 뒤에 값을 추가
  - ```<input type="text" class="text" th:attrappend="class=' large'" /> ```
  - -> ```<input type="text" class="text large" />```
- ```th:attrprepend``` : 속성 값 뒤에 값을 추가
  - ```<input type="text" class="text" th:attrprepend="class='large '" />```
  - -> ```<input type="text" class="large text" />```
- ```th:classappend``` : 속성 값 뒤에 값을 추가
  - ```<input type="text" class="text" th:classappend="large" />```
  - -> ```<input type="text" class="text large" />```

**checked 처리**
- HTML에서 checked = false 인 경우에도 checked 속성이 있기 때문에 체크처리가 되어버린다.
- 타임리프는 th:checked 값이 false인 경우 checked 속성 자체를 없애버린다.
- ```<input type="checkbox" name="active" th:checked="false" />```
- 렌더링 후 -> ```<input type="checkbox" name="active" />```
- - -
## 반복

**반복 기능**
- ```<tr th:each="user,userStat : ${users}">```
- ${users} 컬렉션의 값을 하나씩 꺼내서 왼쪽 변수(user)에 담아서 태그를 반복한다.
- th:each에는 List뿐만 아니라 iterable, enumeration을 구현한 객체도 사용가능하다. Map도 가능한데 그러면 Map.Entity가 변수에 담긴다.
- userStat 변수 : 해당 반복문의 반복 상태를 확인할 수 있다.
- 두번쨰 파라미터는 생략 가능하며 그러면 지정 변수명(user) + Stat가 된다.
- userStat 기능
  - index : 0부터 시작하는 값
  - count : 1부터 시작하는 값
  - size : 전체 사이즈
  - even , odd : 홀수, 짝수 여부( boolean )
  - first , last :처음, 마지막 여부( boolean )
  - current : 현재 객체

- - -
## 조건부 평가
- 조건식 : if, unless(if문의 반대)
  - ```<span th:text="'미성년자'" th:if="${user.age lt 20}">```
  - ```<span th:text="'미성년자'" th:unless="${user.age ge 20}">```
  - 만약 해당 조건에 만족하지 않으면 태그 자체를 렌더링 하지 않는다.
- switch    
  - case="*"는 만족하는 조건이 없을 때 사용하는 디폴트이다.
- - -
## 주석
- html 주석 : ```<!-- -->``` 렌더링하지 않고 그대로 남겨둔다.
- 타임리프 파서 주석 : ```<!--/*```, ```*/-->```, 아니면 ```<!--/*-->```, ```<!--*/-->``` 로 해도 된다. 
  - 이 타임리프 주석은 렌더링에서 주석 부분을 제거한다.
- 타임리프 프로토타입 주석 : ```<!--/*/``` ~ ```/*/-->```
  - HTMl 파일을 열면 주석처리가 되지만 타임리프를 렌더링한 경우에만 보이는 기능이다.

- - -
## 블록
- ```<th:block> ``` : 타임리프 자체의 유일한 태그이다.
- 태그안에 속성으로 사용하기 애매한 경우 사용하면 된다.
- ```<th:block th:each="user : ${users}">```
- ```</th:block>```

- - -
## 자바스크립트 인라인
- ```<script th:inline="javascript">```
- 인라인을 사용하면 렌더링 후 문자 타입인 경우 " 를 포함해준다. 추가로 js에서 문제될 수 있는 특문은 이스케이프 처리해준다. ex) ```" -> \"```

**자바스크립트 내추럴 템플릿**
- 주석을 활용해서 기능을 사용할 수 있다.
- ```var username2 = /*[[${user.username}]]*/ "test username"```
- 인라인 사용 후 -> ```var username2 = "userA"```
- 인라인을 사용하면 원하는 내용으로 교체되는 것을 볼 수있다.

**객체**
- 인라인 기능을 사용하면 객체를 JSON으로 자동 변환해준다.
- 인라인을 사용하지 않으면 toString() 호출된다.

**자바스크립트 인라인 each**
- 자바스크립트 인라인은 each를 지원하는데, 다음과 같이 사용한다.
- ```[# th:each="user, stat : ${users}"]```
- ```var user[[${stat.count}]] = [[${user}]];```
- ```[/]```
- - -
## 템플릿 조각
- 웹페이지에서 공통 영역을 효율적으로 관리하기 위해 타임리프는 템플릿 조각과 레이아웃 기능을 지원한다.

**템플릿 조각**  
- footer.html
```html
<footer th:fragment="copy">
    푸터 자리 입니다.
</footer>
<footer th:fragment="copyParam (param1, param2)">
    <p>파라미터 자리 입니다.</p>
    <p th:text="${param1}"></p>
    <p th:text="${param2}"></p>
</footer>
```
- 메서드 이름을 주듯이 fragment에 이름을 주고 다른 html파일에서 불러와서 사용하는 것이다.
- fragmentMain.html
```html
<div th:insert="~{template/fragment/footer :: copy}"></div>

<div th:replace="~{template/fragment/footer :: copy}"></div>

<div th:replace="~{template/fragment/footer :: copyParam ('데이터1', '데이터2')}"></div>
```
- ```th : insert``` 를 사용하면 현재 태그 내부에 추가된다.
- ```th : replace``` 를 사용하면 현재 태그를 대체한다.
- ~ {} 를 사용하는게 원칙이지만 생략할 수 있다.
- 파라미터를 전달해서 동적으로 렌더링 할 수도 있다.

**템플릿 레이아웃1**
- 위에서는 조각을 가져와서 사용했다면 코드 조각을 레이아웃에 넘겨서 사용해보자
- base.html
```html
<head th:fragment="common_header(title, link)">

    <title th:replace="${title}">레이아웃 타이틀</title>

    <th:block th:replace="${link}"/>

</head>
```
- 이 base를 레이아웃으로 사용하고 title과 link에 원하는 코드 조각을 넘길 것이다.
- layoutMain.html
```html
<head th:replace="template/layout/base :: common_header(~{::title}, ~{::link})">
    <title>메인 타이틀</title>
    <link rel="stylesheet" th:href="@{/css/bootstrap.min.css}">
    <link rel="stylesheet" th:href="@{/themes/smoothness/jquery-ui.css}">
</head>
```
- 참고로 ~{}는 생략 가능하다.
- 템플릿 조각은 template/fragment/footer :: copyParam ('데이터1', '데이터2')
- 템플릿 레이아웃은 template/layout/base :: common_header(~{::title}, ~{::link})
- 이다. ~{::} 를 주의하자.
- 이렇게 하면 common_header 레이아웃에 ::title -> 타이틀 태그와 ::link -> 링크 태그를 붙여준다.
- 현재 페이지의 태그들을 레이아웃으로 전달한다.

**템플릿 레이아웃2**
- 위의 개념을 ```<head>``` 정도에 적용하는게 아닌 ```<html>``` 에 적용할 수도 있다.
- layoutFile.html
```html
<html th:fragment="layout (title, content)" xmlns:th="http://www.thymeleaf.org">
<head>
    <title th:replace="${title}">레이아웃 타이틀</title>
</head>
<body>
<div th:replace="${content}">
</div>
```
- layoutExtendMain.html
```html
<html th:replace="template/layoutExtend/layoutFile :: layout(~{::title}, ~{::section})"
      xmlns:th="http://www.thymeleaf.org">
<head>
    <title>메인 페이지 타이틀</title>
</head>
<body>
<section>
    <p>메인 페이지 컨텐츠</p>
    <div>메인 페이지 포함 내용</div>
</section>
</body>
```
- 레이아웃파일에 기본 레이아웃을 가지고 있는데, ```<html>``` 에 fragment 속성을 정의했다.
- 이 레이아웃파일을 기준으로 하고 필요한 부분을 부분부분 변경하는 것으로 이해하면 된다.
























