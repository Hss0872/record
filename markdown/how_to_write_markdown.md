# 마크다운 문법
## 1.1 헤더
- 글머리 : 1~6까지 지원
<pre>
<code>
# Hi  H1
## Hi  H2
### Hi  H3
#### Hi  H4
##### Hi  H5
###### Hi  H6
</code>
</pre>
# Hi  H1
## Hi  H2
### Hi  H3
#### Hi  H4
##### Hi  H5
###### Hi  H6

- - -

## 1.2 목록
- 순서 있는 목록
<pre>
<code>
1. 첫번째
3. 세번째
2. 두번째

</code>
</pre>
1. 첫번째
3. 세번째
2. 두번째  
  
순서대로 적지 않아도 내림차순으로 입력된다.
- 순서 없는 목록
<pre>
<code>
- 첫번째
- 두번째
- 세번째
  - 3.1
    - 3.1.1
</code>
</pre>

- 첫번째
- 두번째
- 세번째
  - 3.1
    - 3.1.1


- - -
## 1.3 코드 블럭 사용
<pre>
<code>
public String method() {
    return "ok";
}
</code>
</pre>

- \<pre> 와 \<code> 를 적어주고 안에 코드를 작성하면 된다.
- \``` + 언어를 선언해주면 문법 강조를 해줄 수 있다.


<pre>
<code>
```java
public String method() {
    return "ok";
}
```
</code>
</pre>
```java
public String method() {
    return "ok";
}
```

- - -
## 1.4 줄바꿈, 인용, 강조

- 줄바꿈 : 문장 끝에서 띄어쓰기를 2번 하거나 한줄을 비워야 줄바꿈이 된다.
<pre>
class  
method
variable
</pre>
class  
method
variable
- class 다음에 띄어쓰기 2번을 했기 때문에 줄바꿈이 되었다.

<pre>
class

method
</pre>
class

method

**이렇게 한 줄을 비우면 줄바꿈이 된다.**

- 인용
<pre>
class !!! 
> variable
> method
</pre>
class !!!
> variable  
> method

- 강조

<pre>
*This is a text*
_This is a text_

**This is a text**
__This is a text__

*you **can** combine them*
</pre>
*This is a text*  
_This is a text_

**This is a text**  
__This is a text__

*you **can** combine them*

- - -
## 1.5 테이블

<pre>
First Header | Second Header
--- | ---
content cell 1 | content cell 2
content column 1 | content column 2
</pre>
First Header | Second Header
--- | ---
content cell 1 | content cell 2
content column 1 | content column 2

- - -
## 1.6 링크
- 참조링크
<pre>
[link keyword][id]

[id] : URL "Optional Title here"

// code
Link : [Google][googleLink]

[googleLink]: https://www.google.com/
</pre>
Link : [Google][googleLink]

[googleLink]: https://www.google.com/

- 외부링크
<pre>
사용문법 : [Google](link)
적용 예시 : [Google](https://www.google.com/)
</pre>
[Google](https://www.google.com/)


- 자동연결
<pre>
일반적인 URL 혹은 이메일주소인 경우 적절한 형식으로 링크를 형성한다. (<띄어쓰기 사용x>) 


* 외부링크 :  https://www.google.com/
* 이메일 링크 : hss0872@chungbuk.ac.kr
</pre>
* 외부링크 :  https://www.google.com/
* 이메일 링크 : hss0872@chungbuk.ac.kr

- - -
## 1.7 이미지
<pre>
![Alt text](/markdown/image/wolves-g7cefb945a_1280.jpg)
</pre>
![Alt text](/markdown/image/wolves-g7cefb945a_1280.jpg)
- 경로를 잘 설정해주자!
- 사이즈 조절 기능은 없기 때문에 <code>\<img width="" height="">\</img></code> 를 이용한다.

<img src="image/wolves-g7cefb945a_1280.jpg" width="200" height="100" title="px(픽셀)크기설정" alt="RubberDuck"></img>

- - -
# 참고 문서
- [ihoneymon님의 마크다운 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601)