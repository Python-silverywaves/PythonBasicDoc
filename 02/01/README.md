# 숫자 자료형

> print()
```
  - () 안 내용(값)을 화면에 출력하라는 뜻의 명령어
  
  - 다른 프로그래밍 언어와는 다르게 파이썬은 명령어 끝에 세미콜론(;)을 붙이지 않음
```

<br>

숫자 자료형이란
---
- 숫자로 된 데이터

- 종류

  - 1, 2, 3 과 같은 정수형

  - 1.2, 3.14 와 같은 실수형

- 출력

  - 별도 표시 없이 소괄호(()) 안에 값을 그대로 넣으면 됨
 
  - 간단한 수식을 넣을 경우
 
    - 곱하기 연산을 : 수학에서 쓰는 ×(곱셈 기호)가 아니라 *(애스터리스크, asterisk) 사용
   
    - 나누기 연산을 : ÷(나눗셈 기호)가 아니라 /(슬래시, slash) 사용
   
      - 나누기 연산을 하면 결과는 소수점을 포함한 실수 형태

<br>

> ch2.py
```
  print(5)
```

> 실행결과
```
  5
```

<br>

> ch2.py
```
  print(-10)
  print(3.14)
  print(1000)
```

> 실행결과
```
  -10
  3.14
  1000
```

<br>

> ch2.py
```
  print(5 + 3)
  print(2 * 8)
  print(6 / 3)
  print(3 * (3 + 1))
```

> 실행결과
```
  8
  16
  2.0
  12
```

<br>

#### 💡 실행할 때 오류 발생 시
> 프로그램을 실행할 때 실수로 한 줄 실행 단축키(Shift + Enter)가 눌려진 경우
```
  & C:/Python38/python.exe c:/Users/Desktop/PythonWorkspace/ch2.py
  File "<stdin>", line 1
  & C:/Python38/python.exe c:/Users/Desktop/PythonWorkspace/ch2.py
  ^
  SyntaxError: invalid syntax
  #SyntaxError #invalid syntax #stdin #line 1
```
- 터미널 창의 오른쪽 위에 있는 쓰레기통 모양 아이콘을 터미널 창이 모두 닫힐 때까지 계속 누른 후 다시 실행

- 터미널 창에서 exit()라고 입력한 후 Enter

<br>

### 연습 문제
#### ✏️ 1. 다음 중 숫자 자료형 -10을 출력하기 위한 방법으로 알맞은 것은?
```
  ① print(- + 10)
  
  ② print(-10)
  
  ③ print("-10")
  
  ④ print(10-)
```

<details>
  <summary>정답</summary>

<br>

> ② print(-10)

</details>

<br>

