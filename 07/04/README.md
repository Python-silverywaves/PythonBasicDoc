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

#### 지역변수 확인
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

















