## html 문법
- - -
```<h1>``` : 제목 크기

```<p>``` : 하나의 text 단락으로 본다. 끝나고 줄바꿈 해준다.

```<em>``` : 강조 표시

```<strong> ``` : 진하게 표시

```<br>``` : 줄바꿈

```<b>``` : 진하게 표시 strong과 동일하지만 차이는 strong은 강조의 표시가 있지만 b는 진하게 표시할 뿐이다. 눈으로 볼 때는 큰 차이가 없지만 화면 낭독기, 다른 기기에서는 다르게 표현할 수 있는 여지가 있다.

```<hr>``` : 분위기 전환 느낌 ? - - -과 같다.

```<ol>``` : ordered list -> 순서가 있는 목록이다. 만약 abcd를 넣고 싶다면 type="a"를 추가하면 된다.

```<ul>``` : 순서가 없는 목록이다.

#### 표 만들기

```<caption>``` : 표 제목

```<table>``` : 표 전체

```<tr>``` : 행

```<td>``` : 셀

```<th>``` : 제목 셀

```<td rowspan="합칠 셀의 개수">``` : 행을 합칠 때 사용

```<td colspan="합칠 셀의 개수">``` : 열을 합칠 때 사용

#### 이미지

```<img src="" alt="">``` 이미지 삽입

```<audio src="">``` : controls를 사용하면 재생막대를 생성해준다.

```<video src="">``` : 비디오 삽입

```<audio> <video>``` : 태그의 속성
  
- controls : 컨트롤 바 표시
- autoplay : 오디오나 비디오 자동 재생 (크롬 브라우저에서 만약 비디오를 자동재생 하고 싶다면 muted를 써서 소리를 제거해야 한다.)
- muted : 오디오나 비디오의 소리를 제거
- preload : 페이지를 불러올 때 오디오나 비디오 파일을 어떻게 로딩할 것인지 지정한다. 기본값은 preload:"auto" 이다.

#### 폼 삽입하기

```
<fieldset>
  <legend>그룹 이름</legend>
</fieldset>
```

- fieldset, legend 태그 : 하나의 폼 안에 여러 구역을 나누어 표시할 때 사용한다. 사용자가 입력하기도 편하고 화면도 깔끔하게 정리할 수 있다.

```<labal> 아이디 : <input type="text"></label>``` : label이라는 태그를 통해 글자와 연결된 필드를 명확하게 확인할 수 있다. 소스가 복잡한 경우 ```<label for="id">``` 를 사용해서 label 태그를 따로 사용할 수 있다.

- 체크박스 : 여러개 선택 가능 

- ```<input type="checkbox" value="f_3">가정용 3kg <input type="number"> 개 ```

- 라디오 : 하나만 선택 가능 같은 그룹임을 지정해주기 위해 name을 동일하게 지정해주면 된다.

#### 날짜와 시간

```<input type="date">``` : 날짜

```<input type="month">``` : 시간

- min, max 속성을 사용해서 제한을 둘 수 있다. 브라우저마다 지원하는 것이 다르니 따로 확인해볼 것 
- caniuse.com 태그를 검색하면 어떤 브라우저에서 지원하는지 확인할 수 있다.

```<input type="hidden">``` : 사용자에겐 보이지 않지만 여러 정보들을 히든 필드에 감춰서 서버로 보내지게 된다. 폼에서 많이 사용된다.

- required : 필수 필드
- readonly : 텍스트 필드를 지우지 못하게 고정
- autofocus : 해당 화면으로 이동 시 자동으로 커서 이동

#### 셀렉트 메뉴 만들기

```
<select name="" id="">
  <option value="spectial_3" selected>선물용 3kg</option>
  <option value="spectial_5">선물용 5kg</option>
  <option value="family_3">가정용 3kg</option>
  <option value="family_5">가정용 5kg</option>
</select>
```