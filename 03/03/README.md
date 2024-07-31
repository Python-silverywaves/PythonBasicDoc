# 변수로 연산하기
변수와 연산자를 함께 사용
---
> 수식을 number라는 변수에 넣고 변수의 값을 출력
```
  number = 2 + 3 * 4
  print(number)
```

<br>

> 실행결과
```
  14
```

<br>

- 위 코드에 2를 더하려면?
> 1. 수식 추가
```
  number = 2 + 3 * 4
  print(number)
  number = 2 + 3 * 4 + 2
  print(number)
```

> 2. 변수 활용
```
  number = 2 + 3 * 4
  print(number)
  number = number + 2   # (2 + 3 * 4) + 2
  print(number)
```

<br>

> 실행결과
```
  14
  16
```

<br>

복합 대입 연산자(augmented assignment operator)
---
- 대입 연산자 + 산술 연산자

<br>

|연산자|의미|예|
|:-:|-|-|
|+=|연산자 왼쪽 값에 오른쪽 값을 더한 후 왼쪽 값에 대입|number = number + 2 → number += 2|
|-=|연산자 왼쪽 값에서 오른쪽 값을 뺀 후 왼쪽 값에 대입|number = number - 2 → number -= 2|
|*=|연산자 왼쪽 값에 오른쪽 값을 곱한 후 왼쪽 값에 대입|number = number * 2 → number *= 2|
|/=|연산자 왼쪽 값을 오른쪽 값으로 나눈 후 왼쪽 값에 대입|number = number / 2 → number /= 2|
|**=|연산자 왼쪽 값을 오른쪽 값으로 거듭제곱한 후 왼쪽 값에 대입|number = number ** 2 → number **= 2|
|//=|연산자 왼쪽 값을 오른쪽 값으로 나눈 후 몫을 왼쪽 값에 대입|number = number // 2 → number //= 2|
|%=|연산자 왼쪽 값을 오른쪽 값으로 나눈 후 나머지를 왼쪽 값에 대입|number = number % 2 → number %= 2|

<br>

> 복합 대입 연산자를 적용
```
  number = 2 + 3 * 4
  print(number)
  # number = number + 2
  # print(number)
  number += 2 # number = number + 2와 동일
  print(number)
```

<br>

> 실행결과
```
  14
  16
```

<br>

> 현재 number 변수의 값인 16을 기준으로 순서대로 연산한 결과 확인
```
  number -= 2 # number = number - 2와 동일
  print(number)
  number *= 2 # number = number * 2와 동일
  print(number)
  number /= 2 # number = number / 2와 동일
  print(number)
  number **= 2 # number = number ** 2와 동일
  print(number)
  number //= 2 # number = number // 2와 동일
  print(number)
  number %= 2 # number = number % 2와 동일
  print(number)
```

<br>

> 실행결과
```
  14
  28
  14.0
  196.0
  98.0
  0.0
```
- 정수로 나누기 연산을 하면 결과는 소수점을 포함한 실수 형태

  - number / 2 이후부터는 결과가 14.0, 196.0과 같이 실수 형태로 출력

<br>

###  연습문제
#### ✏️ 1. 다음과 같은 실행결과를 얻기 위해 [갸]에 들어갈 코드로 알맞은 것은?
```
  num = 3
  [가]
  print(num)
```

> 실행결과
```
  6
```

```
  ① num += 2
  
  ② num *= 2
  
  ③ num + 3
  
  ④ num == 2
```

<details>
  <summary>정답</summary>

<br>

> ② num *= 2
```
  실행결과가 6이므로 num 변수의 값인 3에 2를 곱해야 함
  
  ③처럼 + 3으로 연산하려면 =을 함께 사용해 num += 3으로 작성
```

</details>

<br>
