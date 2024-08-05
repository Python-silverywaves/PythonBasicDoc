# 사용자 정의 예외 처리하기
- 사용자가 직접 오류를 정의해 예외 처리하기

> 두 자리 이상의 수로 잘못 입력했을 때 사용자 입력 중 어디가 잘못됐는지를 알려 주도록 코드 수정
```
  class BigNumberError(Exception): # 사용자 정의 예외 처리, Exception 클래스 상속
      pass
  try:
      print("한 자리 숫자 나누기 전용 계산기입니다.")
      num1 = int(input("첫 번째 숫자를 입력하세요 : "))
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
      if num1 >= 10 or num2 >= 10: # 입력받은 수가 한 자리인지 확인
          # raise ValueError
          raise BigNumberError
      print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2))) 
  except ValueError:
      print("값을 잘못 입력했습니다. 한 자리 숫자만 입력하세요.")
  except BigNumberError: # 사용자 정의 예외 처리
      print("오류가 발생했습니다. 한 자리 숫자만 입력하세요.")
```
- 두 자리 이상의 수를 입력할 때 발생하는 오류라는 의미로 BigNumberError라는 클래스 생성

  - 클래스 내용은 일단 pass 문

- Exception이라는 클래스를 상속

  - 코드에서 새로운 오류를 정의해 예외 처리하려면 상속받아야하는 파이썬에 포함된 클래스
 
- 입력값이 10 이상인지를 확인하는 if 문

  - ValueError 대신 새롭게 정의한 BigNumberError를 발생
  
  - except 문을 추가해 예외 처리

<br>

> 실행결과
```
  한 자리 숫자 나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 10
  두 번째 숫자를 입력하세요 : 5
  오류가 발생했습니다. 한 자리 숫자만 입력하세요.
```
- 10과 5를 순차적으로 입력

- BigNumberError가 발생하고 예외 처리가 실행

- 마지막에 추가한 except 문의 안내 문구를 출력

<br>

> BigNumberError 클래스 완성
```
  class BigNumberError(Exception): # 사용자 정의 예외 처리, Exception 클래스 상속
      def __init__(self, msg):
          self.msg = msg
  
      def __str__(self):
          return self.msg
```
- pass 문 대신 __init__() 생성자와 __str__() 메서드를 추가

  - 생성자에서는 오류 메시지를 의미하는 msg를 전달받아 인스턴스 변수로 설정
 
  - 메서드에서는 인스턴스 변수 msg를 반환
 
- BigNumberError를 발생시킬 때 필요한 문구를 추가해 더 자세한 오류 내용을 출력

<br>

> 오류가 발생하는 시점에 어떤 값을 입력했는지 출력
```
  class BigNumberError(Exception): # 사용자 정의 예외 처리
      def __init__(self, msg):
          self.msg = msg
  
      def __str__(self):
          return self.msg
  
  try:
      print("한 자리 숫자 나누기 전용 계산기입니다.")
      num1 = int(input("첫 번째 숫자를 입력하세요 : "))
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
      if num1 >= 10 or num2 >= 10: # 입력받은 수가 한 자리인지 확인
          # 자세한 오류 메시지
          raise BigNumberError("입력값 : {0}, {1}".format(num1, num2))
      print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))
  except ValueError:
      print("값을 잘못 입력했습니다. 한 자리 숫자만 입력하세요.")
  except BigNumberError as err: # 사용자 정의 예외 처리
      print("오류가 발생했습니다. 한 자리 숫자만 입력하세요.")
      print(err) # 오류 메시지 출력
```
- try 문에서 BigNumberError를 발생시키는 부분에 입력받은 두 값을 문자열 형태로 넣기

  - __init__() 생성자의 msg로 들어감

- __str__() 메서드에 의해 msg 인스턴스 변수가 반환

- except 문에서는 as를 이용해 err이라는 이름으로 반환된 오류 내용을 받음

- print() 문으로 출력

<br>

> 실행결과
```
  한 자리 숫자 나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 10
  두 번째 숫자를 입력하세요 : 5
  오류가 발생했습니다. 한 자리 숫자만 입력하세요.
  입력값 : 10, 5
```
- 오류 내용과 함께 사용자가 어떤 값을 입력했는지도 함께 출력

<br>

> 오류 메시지 가공
```
  class BigNumberError(Exception): # 사용자 정의 오류
      def __init__(self, msg):
          self.msg = msg
  
      def __str__(self):
          return "[오류 코드 001] " + self.msg # 오류 메시지 가공
  try:
      print("한 자리 숫자 나누기 전용 계산기입니다.")
      num1 = int(input("첫 번째 숫자를 입력하세요 : "))
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
      if num1 >= 10 or num2 >= 10: # 입력받은 수가 한 자리인지 확인
          # 자세한 오류 메시지
          raise BigNumberError("입력값 : {0}, {1}".format(num1, num2))
      print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))
  except ValueError:
      print("값을 잘못 입력했습니다. 한 자리 숫자만 입력하세요.")
  except BigNumberError as err: # 사용자 정의 예외 처리
      print("오류가 발생했습니다. 한 자리 숫자만 입력하세요.")
      print(err) # 오류 메시지 출력
```
- __init__() 생성자와 __str__() 메서드는 따로 정의하지 않고 그냥 pass로 두어도 동일하게 동작하긴 함

  - 생성자에서 추가로 어떤 작업을 해야 한다거나 __str__() 메서드에서 오류 메시지를 오류 코드와 함께 출력하고 싶은 경우

    - 코드 수정

- 프로그램에 오류 코드를 다음과 같이 정의했을 때 BigNumberError에서는 오류 코드 001을 출력

> 오류 코드
```
  [001 : 두 자리 숫자가 입력됨]
  
  [002 : 문자열이 입력됨]
  
  [003 : 공백이 입력됨]
```

<br>

> 실행결과
```
  한 자리 숫자 나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 10
  두 번째 숫자를 입력하세요 : 5
  오류가 발생했습니다. 한 자리 숫자만 입력하세요.
  [오류 코드 001] 입력값 : 10, 5
```

<br>

#### 📌 스페셜 메서드(special method)
```
  __init__()나 __str__()처럼 이름 앞뒤로 언더바(_)가 2개씩 붙은 형태의 메서드
  
  언더바가 2개 들어간다는 의미에서 던더 메서드(dunder method: double underscore method)라고도 함
  
  특별한 역할을 수행하기 위해 별도 처리를 하는 메서드
  
  
  __init__() 메서드는 객체가 생성될 때 자동으로 호출
  
  __str__() 메서드는 print() 함수로 객체를 출력할 때 호출

  __len__() 메서드는 객체 길이를 구할 때 호출

  __contains__() 메서드는 객체가 특정 요소를 포함하는지 확인할 때 호출
```

<br>

> ex
```
  class SpecialClass():
      def __init__(self):
          print("특별한 생성자")
  
      def __str__(self):
          return "특별한 메서드"
  
  s = SpecialClass() # 특별한 생성자 출력
  print(s) # 특별한 메서드 출력
```

<br>

> 실행결과
```
  특별한 생성자
  특별한 메서드
```
- 객체가 생성될 때 자동으로 __init__() 메서드가 호출되어 특별한 생성자가 출력

- print() 함수로 객체 s를 출력하면 __str__() 메서드가 호출되어 특별한 메서드가 출력

<br>

### 연습문제
#### ✏️ 1. 새로운 사용자 정의 예외 클래스인 MyError를 만들기 위해 가에 들어갈 부모 클래스로 올바른 것은?
```
  class MyError( 가  ):
      pass
```
```
  ① Base
  
  ② Error
  
  ③ Except
  
  ④ Exception
```

<details>
  <summary>정답</summary>

<br>

> ④ Exception

</details>

<br>










