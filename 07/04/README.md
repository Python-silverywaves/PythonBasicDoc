# 변수의 범위: 지역변수와 전역변수
지역변수(local variable)
---
- 함수 안(지역)에서만 사용할 수 있는 변수

- 매개변수를 포함해 함수 안에서 새롭게 정의하는 변수는 모두 해당

<br>

전역변수(global variable)
---
- 모든 곳(전역)에서 사용할 수 있는 변수

<br>

### ex
> 영화관의 3D 안경 보관함에 3D 안경이 10개 있고 관객 2명에게 대여했을 때 남은 안경이 몇 개인지 구하는 프로그램
```
  glasses = 10 # 전체 3D 안경 개수: 10개
  
  def rent(people): # 3D 안경을 대여한 관객 수
      glasses = glasses - people # 잔여 3D 안경 개수 = 전체 개수 - 대여한 개수
      print("[함수 내부] 남은 3D 안경 개수: {0}".format(glasses))
  
  print("전체 3D 안경 개수: {0}".format(glasses))
  rent(2) # 3D 안경을 대여한 관객이 2명일 때
  print("남은 3D 안경 개수: {0}".format(glasses))
```

<br>

> 실행결과
```
  UnboundLocalError: local variable ‘glasses’ referenced before assignment
```
- 오류 발생
  
  - glasses라는 변수가 아직 할당되지 않았는데 사용됐다는 뜻

- [7.2.1 실습: 입금하기](../02)에서 함수를 정의하고 호출할 때 이름이 같은 balance 변수를 사용
  - 두 변수는 같은 변수 X
  
  - 함수에 정의한 balance 변수는 전달값을 받는 매개변수
  
    - 함수 안에서만 사용 가능
   
    - 지역변수
  
  - rent() 함수 안에서 사용하는 glasses 변수도 함수 외부에 정의한 glasses와는 아무 상관없는, rent() 함수 안에서 새로 만들어진 지역변수
  
    - 값을 넣어 정의하기 전에 glasses - people이라는 연산을 하려 해서 오류가 발생

<br>

### 지역변수 확인
> rent() 함수 안에 값 20을 넣어 glasses 변수를 정의하고 다시 실행
```
  glasses = 10
  
  def rent(people):
      glasses = 20 # 변수 정의 추가
      glasses = glasses - people
      print("[함수 내부] 남은 3D 안경 개수: {0}".format(glasses))
  
  print("전체 3D 안경 개수: {0}".format(glasses))
  rent(2)
  print("남은 3D 안경 개수: {0}".format(glasses))
```

<br>

> 실행결과
```
  전체 3D 안경 개수: 10
  [함수 내부] 남은 3D 안경 개수: 18
  남은 3D 안경 개수: 10
```
- 정상 작동

- 함수 안에서는 glasses 변수에 20을 넣은 뒤 안경 대여 관객 수인 2를 빼서 18로 줄어듦

- 전체 안경 개수와 남은 안경 개수는 10으로 변함 x

  - 함수 안에서 정의한 glasses 변수가 지역변수이기 때문

  - 전역 공간에 만들어진 glasses 변수와 이름은 같지만, 서로 다른 변수

  - 전역변수인 glasses의 값에는 아무런 영향 X

<br>

### global
- global을 변수 앞에 붙이면 전역변수를 함수 안에서 사용하겠다는 의미

  - 함수 안에 global glasses라고 작성하면 전역 공간에 정의한 변수를 함수 안에서 그대로 사용 및 값 변경 가능

<br>

> 수정 코드
```
  glasses = 10
  
  def rent(people):
      global glasses # 전역 공간에 있는 glasses 변수를 함수 안에서 사용하겠다는 표시
      glasses = glasses - people
      print("[함수 내부] 남은 3D 안경 개수: {0}".format(glasses))
  
  print("전체 3D 안경 개수: {0}".format(glasses))
  rent(2)
  print("남은 3D 안경 개수: {0}".format(glasses))
```

<br>

> 실행결과
```
  전체 3D 안경 개수: 10
  [함수 내부] 남은 3D 안경 개수: 8
  남은 3D 안경 개수: 8
```
- 보관함에 남은 안경 개수를 제대로 출력

- 함수 안에 전역변수를 자주 사용하면 코드 관리 복잡

  - 꼭 필요한 경우가 아니라면 되도록 사용 X

<br>

### 전달값과 반환값을 활용해 전역변수가 없는 버전으로 수정
- 반환 의미를 담아 rent_return()이라는 새로운 함수로 정의

<br>

> 수정 코드
```
  glasses = 10
   
  
  def rent_return(glasses, people): # 전체 3D 안경 수와 대여 관객 수를 전달받음
      glasses = glasses - people # 전달값을 담은 glasses 사용
      print("[함수 내부] 남은 3D 안경 개수: {0}".format(glasses))
      return glasses
  print("전체 3D 안경 개수: {0}".format(glasses))
  glasses = rent_return(glasses, 2) # 함수 안에서 수정된 glasses 값을 반환받음
  print("남은 3D 안경 개수: {0}".format(glasses))
```

<br>

> 실행결과
```
  전체 3D 안경 개수: 10
  [함수 내부] 남은 3D 안경 개수: 8
  남은 3D 안경 개수: 8
```
- 함수를 정의할 때 전달값을 잘 이용하면 함수 외부 상황은 몰라도 함수 기능에 충실하면서도 간결하게 작성 가능

- 잘 만든 함수는 언젠가 다른 프로그램에서 같은 기능이 필요할 때 그대로 활용 가능

<br>

### 연습문제
#### ✏️ 1. 다음 중 지역변수에 대한 설명으로 잘못된 것은?
```
  ① 함수 내에 정의된 변수는 지역변수다.
  
  ② 지역변수는 외부에서 접근할 수 없다.
  
  ③ 함수가 호출된 후에는 호출된 함수 안에 정의한 지역변수도 외부에서 접근할 수 있다.
  
  ④ 서로 다른 함수에서 같은 이름의 지역변수를 정의할 수 있으며, 이때 두 변수는 서로 관련이 없다.
```

<details>
  <summary>정답</summary>

<br>

> ③ 함수가 호출된 후에는 호출된 함수 안에 정의한 지역변수도 외부에서 접근할 수 있다.
```
  함수 안에 정의한 지역변수는 함수 안에서만 접근
```

</details>

<br>

#### ✏️ 2. 다음 코드의 실행결과로 올바른 것은?
```
  x = 3
  def add():
      x = 6
      x += 3
  add()
  print(x)
```
```
  ① 3
  
  ② 6
  
  ③ 9
  
  ④ 오류 발생
```

<details>
  <summary>정답</summary>

<br>

> ① 3

</details>

<br>
