# 마무리
## 1. 연산자
- 연산자는 프로그래밍에서 연산할 때 사용하는 기호

  • 산술 연산자: 덧셈, 뺄셈, 곱셈, 나눗셈 등 수를 연산하는 데 사용
  
  • 비교 연산자: 값의 크기를 비교할 때 사용
  
  • 논리 연산자: 수식, 조건 등에서 값이 참인지 거짓인지 판단할 때 사용

<br>

## 2. 연산자의 우선순위
- 연산자에는 우선순위가 있어서 수식을 어떻게 작성하느냐에 따라 연산 순서가 달라질 수 있음

<br>

> 주요 우선순위

|-|
|-|
|![image](https://github.com/user-attachments/assets/62c88da2-7f73-43ee-b2f4-52b8ead78da1)|

<br>

## 3. 변수로 연산하기
- 연산을 쉽게 하기 위해 변수에 연산 결과를 저장한 뒤 새로운 연산에 활용 가능

  - 복합 대입 연산자를 사용하면 더욱 간소한 형태로 연산이 가능

<br>

|-|
|-|
|![image](https://github.com/user-attachments/assets/1ef9d465-1938-4229-b267-6d23b98528f5)|

<br>

## 4. 함수로 연산하기
- 파이썬에서는 다양한 연산을 편리하게 할 수 있도록 여러 함수를 제공

<br>

|-|
|-|
|![image](https://github.com/user-attachments/assets/d4ba865c-5493-429f-8041-a2209b522067)|

<br>

## 5. math 모듈
- math 모듈에도 숫자 연산을 수행하는 함수들 有

- 모듈의 기능을 사용하려면 다음과 같이 import를 먼저 진행

<br>

> 형식
```
from 모듈명 import 기능
```

<br>

|-|
|-|
|![image](https://github.com/user-attachments/assets/9e686610-08ff-4c88-80e0-e716509cf1fe)|


<br>

## 6. random 모듈
- random 모듈에는 난수가 필요한 경우에 사용하는 함수들 有

- 함수에 따라 마지막 값을 포함하는지 아닌지가 달라질 수 있으니 주의

<br>

|-|
|-|
|![image](https://github.com/user-attachments/assets/f26d536f-aa2d-4994-a948-7af9d07c49cb)|

<br>

## 연습문제
### 연산자를 이용해 온도 단위를 변환하는 프로그램을 만들어 보세요.
### 조건
  - 섭씨 온도를 저장하기 위한 변수를 만든다.
  
  - 다음 공식을 이용해 섭씨 온도를 화씨 온도로 변환하고 새로운 변수에 저장한다.
  
    - 화씨 온도 = (섭씨 온도 * 9 / 5) + 32
  
  - 섭씨 온도와 화씨 온도를 다음과 같이 출력한다.

<br>

> 실행결과
```
  # 섭씨 온도가 30도일 때
  섭씨 온도 : 30
  화씨 온도 : 86.0
  
  # 섭씨 온도가 10도일 때
  섭씨 온도 : 10
  화씨 온도 : 50.0
```

<br>

<details>
  <summary>정답</summary>

<br>

> 코드
```
  celsius = 30
  fahrenheit = (celsius * 9 / 5) + 32
  print("섭씨 온도 : " + str(celsius))
  print("화씨 온도 : " + str(fahrenheit))
```

</details>
