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
  - 여기서 nullData는 없으므로 기존의 text가 출력된다.




