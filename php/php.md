# PHP 기본 문법

- 모든 기본 문법은 ```<?php ?>``` 안에 작성한다.
- html에 출력하는 방법 2가지
  - ```echo 1;```
  - ```print(1);```

- ',"로 문자열을 표현한다. 만약 '로 문자를 표현한다면 ```"Hello 'w'orld"``` 이렇게 작성해주거나 \를 사용해주면 된다.

- . (concatenation operator) : 좌항과 우항을 결합해서 하나의 문자열을 만들어낸다.
- ex)  ```"Hello "."world"```
- strlen(string $string) : 문자열의 길이 계산
- ``` echo strlen("Hello world");```

- $ : 변수를 선언하는 문자
- ex) ```$name = "HSS" ```
- ``` echo "하이".$name."반갑다.".$name ```
- ```$_GET['key값']``` : url의 매개변수를 받는 방법 (대,소문자 잘 구분할 것)
- nl2br : 자동으로 줄바꿈 태그를 삽입해준다.
- file_get_contents() : 해당 파일의 텍스트 내용을 가져온다.

### 제어문
- var_dump(1) : 입력값을 출력해주는데 입력값의 데이터 타입을 알려준다.
- ``` var_dump(1) -> int(1) ```
- 개발과정에서 사용해주면 좋다.
- == : 비교 연산자
- if() {} else {} : 조건문
- isset() : 값이 set이 되어 있는지 아니면 null이 아닌지 true, false 반환 여러개 값을 체크할 수 있다. 만약 하나라도 값이 없다면 false이다.
- unset : 변수를 제거하는 함수 (만약 함수 안에서 전역변수를 unset하면 로컬 변수만 사라진다. 호출한 환경에서 변수는 unset을 호출하기 전과 같은 값을 유지한다.)

ex)
``` 
$a = "test";
$b = "anoo";

var_dump(isset($a)); //TRUE
var_dump(isset($a, $b)); //TRUE

unset($a);

var_dump(isset($a)); //FALSE
var_dump(isset($a, $b)); //FALSE
```

### 반복문
- expr : 최종적으로 값이 되는 것
- while (expr) {} 
- ``` while($i < 3) {echo $i; $i = $i + 1} ```

### 배열

- ``` array('A', 'B', 'C') ``` : 배열
- ex) ```$coworkers = array('egoing', 'leezche', 'duru');```
- 꺼내는 법 : array[idx]
- count(array) : 배열의 개수 반환
- array_push($a, value1, value2, ...) : 배열 마지막에 데이터를 추가 
- php document에 있는 함수들을 보면 대강 짐작할 수 있다.
- 매개변수 안에 []는 안써도 되지만 []가 없다면 반드시 사용해야 하는 매개변수이다.

- scandir() : 해당 디렉토리 안에 있는 파일 이름을 array로 반환
- ex) ``` $files1 = scandir('/tmp') ```
- " " 안에 $가 들어갔을 때 $뒤에 있는 이름은 변수로 친다.
- ex) ``` echo "<li><a href=\"index.php?id=$list[$i]\">$list[$i]</></li>\n"; ```
