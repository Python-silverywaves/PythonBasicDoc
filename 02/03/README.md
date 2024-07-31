# 불 자료형
불 자료형
---
- 둘 중 하나로만 답이 나올 때 불(boolean)이라는 자료형을 사용

  - ex) 거짓말 탐지기를 사용할 때는 ‘네’와 ‘아니요’ 둘 중 하나로만 답
 
- 코드에서 참과 거짓을 판단할 때 사용

  - 참을 의미하는 True와 거짓을 의미하는 False 값만 가질 수 있음

- boolean 자료형의 값을 넣으면 값을 그대로 출력

<br>

> ch2.py
```
  print(5 > 10)  # 5는 10보다 작은데 크다고 했으니 거짓
  print(5 < 10)  # 참
```

> 실행결과
```
  False
  True
```

<br>

> ch2.py
```
  print(True)
  print(False)
```

> 실행결과
```
  True
  False
```

<br>

연산자(operator)
---
- 프로그래밍에서 값으로 연산을 수행할 때 사용하는 기호

-  +, *, <, > 도 모두 연산자

-  자세한 내용 : [연산자](../../03)

<br>

> '5는 10보다 크지 않다.' 를 수식으로 바꾸면?
```
  5 < 10 은 ‘5는 10보다 작다’는 의미라서 위 문장과 완전히 같지는 않음

  not (5 > 10)
    : 5는 10보다 크다는 것을 부정 = 5는 10보다 크지 않다
```

<br>

### not
- 값을 부정하는 연산자

- 값이 True면 False, 값이 False면 True

<br>

> ch2.py
```
  print(not True)
  print(not False)
```

> 실행결과
```
  False
  True
```

<br>

> ch2.py
```
  print(not (5 > 10))    # 5 > 10은 False, 이를 부정하므로 반대 값인 True 출력
```

> 실행결과
```
  True
```

<br>

### 연습문제
#### ✏️ 1. 다음 중 불 자료형에 대한 설명으로 잘못된 것은?
```
  ① 참과 거짓을 판단할 때 사용한다.
  
  ② True 또는 False만 가지는 자료형이다.
  
  ③ 5 > 10 연산의 결과는 False다.
  
  ④ 불 자료형 앞에 not을 붙이면 None이 된다.
```

<details>
  <summary>정답</summary>

<br>

> ④ 불 자료형 앞에 not을 붙이면 None이 된다.
```
  not은 값을 부정하는 부정 연산자

  불 자료형 앞에 not을 붙이면 True는 False, False는 True
```

</details>

<br>



