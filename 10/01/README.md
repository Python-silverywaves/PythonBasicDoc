# 예외(exception) 처리하기
#### 💡 일상생활에서의 예외 생각해보기
```
  버스에 타서 교통카드를 찍는데 단말기에서 “잔액이 부족합니다.”
  
  버스는 이미 출발했고 지갑에 다른 카드도, 현금도 없는 상황
  
  버스에서 내릴 수도 없고 기사님도 다른 승객들도 쳐다보고 있을 때 어떻게 해야 할까?
```

<br>

예외 처리란
---
> 실생활에서 겪을 수 있는 상황
```
  1. 상품의 배송 주소가 아파트 11층으로 적혀 있는데 실제로는 10층까지만 있는 경우
  
  2. 교통카드 단말기에 교통카드를 갖다 댔는데 잔액이 부족하다고 뜨는 경우
  
  3. 컴퓨터의 계산기 프로그램을 이용하려는데 실수로 숫자 대신 문자를 입력한 경우
  
  4. 어떤 사이트에 접속하려는데 URL 주소를 잘못 적은 경우
  
  5. 쇼핑몰 사이트에 사용자가 많아서 정상적으로 접속되지 않는 경우
```

<br>

### 오류
- 예상치 못한 실수 또는 잘못된 무언가

- 프로그램에서도 굉장히 많은 오류 상황이 발생

  - 이를 어떻게 처리하느냐에 따라 결과물 달라짐
  
    - 완성도가 높고 사용하기 편리한 프로그램
    
    - 갑자기 응답 없음 상태로 있다가 강제 종료돼서 모든 작업이 수포로 돌아가는 프로그램

<br>

### 예외 처리
- 오류 상황에 대처하는 것

- ex) 1번 상황

  - 상품을 받을 사람의 전화번호로 연락해 주소를 확인하면 처리 가능

<br>

예외 처리하기: try-except 문
---
> 사용자로부터 두 수를 입력받아 나누기한 결과를 출력
```
  print("나누기 전용 계산기입니다.")
  num1 = int(input("첫 번째 숫자를 입력하세요 : "))
  num2 = int(input("두 번째 숫자를 입력하세요 : "))
  print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))
```

<br>

> 실행결과1
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 3
  6 / 3 = 2
```
- 프로그램을 실행하고 터미널에 6과 3을 입력하면 계산한 결과를 2라고 출력

<br>

> 실행결과2
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 삼
  Traceback (most recent call last):
    File "c:\PythonWorkspace\ch10.py", line 3, in <module>
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
  ValueError: invalid literal for int() with base 10: '삼'
```
- 숫자가 아닌 문자를 입력하면 오류 메시지를 출력하고 프로그램을 종료

- 나누기 연산 부분에서 오류 발생

  - 입력받은 두 값을 나누기 연산(num1 / num2)하고 이를 다시 int()로 감싸서(int(num1 / num2)) 정수형으로 변환
 
  - 입력한 삼은 정수로 변환할 수 없는 문자

- ValueError : 값이 잘못돼서 발생하는 오류

<br>

### 오류가 발생할 때 예외 처리
- 실행하려는 코드 위에 try 키워드를 적고 뒤에 콜론

- 실행하려는 코드를 모두 들여 써서 try 문의 하위 명령문으로 작성

- 그 아래 except 키워드를 적고 뒤에 어떤 오류에 대한 예외 처리인지를 명시

- 마지막에 콜론

- 다음 줄에 들여쓰기로 예외 처리를 수행할 명령문들은 작성

> 형식
```
  try:
      실행할 명령1
      실행할 명령2
      ...
  except 오류 종류:
      예외 처리 명령1
      예외 처리 명령2
      ...
```

<br>

> 수정코드
```
  try:
      print("나누기 전용 계산기입니다.")
      num1 = int(input("첫 번째 숫자를 입력하세요 : "))
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
      print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))
  except ValueError:
      print("오류 발생! 잘못된 값을 입력했습니다.")
```
- try 문의 하위에 있는 명령문을 실행

- 오류가 발생하면 프로그램을 종료하지 않고 except 문의 오류 종류와 일치하는지 확인

- 일치하면 except 문의 하위 명령문들이 실행

- 오류가 발생하지 않으면 except 문은 실행하지 않고 넘어감

<br>

> 실행결과1
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 3
  6 / 3 = 2
```

<br>

> 실행결과2
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 삼
  오류 발생! 잘못된 값을 입력했습니다.
```
- except 부분의 print() 문이 실행

<br>

오류 메시지를 예외 처리로 출력하기: as
---
- 예외 처리가 한 가지로 끝나지 않는 경우도 있음

- 어떤 문제인지 쉽게 알아볼 수 있는 메시지가 제공되는 오류는 따로 예외 처리 메시지를 정의하지 않고도 간편하게 예외 처리 가능

<br>

> 6과 0을 입력
```
  try:
      print("나누기 전용 계산기입니다.")
      num1 = int(input("첫 번째 숫자를 입력하세요 : "))
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
      print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))
  except ValueError:
      print("오류 발생! 잘못된 값을 입력했습니다.")
```

<br>

> 실행결과
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 0
  Traceback (most recent call last):
    File "c:\PythonWorkspace\ch10.py", line 5, in <module>
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
  ZeroDivisionError: division by zero
```
- ZeroDivisionError : 나누는 수로 0을 넣어서 발생하는 오류

  - 수학에서 어떤 수든 0으로 나눌 수 없기 때문
 
- ValueError와는 다른 종류의 오류라서 기존 except 문만으로는 예외 처리 불가

  - 오류마다 각각 except 문을 추가해 예외 처리를 따로 해야함

<br>

### as
- 오류가 발생할 때 표시하는 오류 메시지를 가져와 출력하도록 예외 처리

  - 예외 처리 형식에서 except 뒤에 as 키워드와 변수명을 추가
 
  - as 뒤에 지정한 변수명으로 오류 메시지를 확인 가능

> 형식
```
  try:
      실행할 명령1 
      실행할 명령2
      ...
  except 오류 종류1
      예외 처리 명령1
      예외 처리 명령2
      ...
  except 오류 종류2 as 변수명:
      예외 처리 명령1
      예외 처리 명령2
      ...
```

<br>

> ZeroDivisionError에 대한 예외 처리를 추가
```
  try:
      print("나누기 전용 계산기입니다.")
      num1 = int(input("첫 번째 숫자를 입력하세요 : "))
      num2 = int(input("두 번째 숫자를 입력하세요 : "))
      print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))
  except ValueError:
      print("오류 발생! 잘못된 값을 입력했습니다.")
  except ZeroDivisionError as err:
      print(err)
```
- ZeroDivisionError에 대한 except 문을 작성

- 뒤에 as 키워드와 err이라는 이름의 변수를 넣고 콜론

- 변수를 print() 문으로 출력

<br>

> 실행결과
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 0
  division by zero
```
- 간단한 문구를 출력하고 프로그램을 종료

<br>

> try 구문 수정
```
  try:
      print("나누기 전용 계산기입니다.")
      nums = []
      nums.append(int(input("첫 번째 숫자를 입력하세요 : ")))
      nums.append(int(input("두 번째 숫자를 입력하세요 : ")))
      nums.append(int(nums[0] / nums[1])) # 연산 결과를 리스트에 추가
      print("{0} / {1} = {2}".format(nums[0], nums[1], nums[2]))
  except ValueError:
      print("오류 발생! 잘못된 값을 입력했습니다.")
  except ZeroDivisionError as err:
      print(err)
```
- nums라는 리스트를 추가로 정의

  - 두 수를 입력받는 부분은 같은데, 입력받은 두 수를 변수가 아닌 nums 리스트에 저장
 
  - 두 수를 연산한 결과도 리스트에 저장
 
- print() 문으로 리스트 값을 순서대로 출력

<br>

> 실행결과
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 3
  6 / 3 = 2
```

<br>

> 연산 결과를 리스트에 추가하는 부분을 코드에 넣지 않으면
```
  try:
      print("나누기 전용 계산기입니다.")
      nums = []
      nums.append(int(input("첫 번째 숫자를 입력하세요 : ")))
      nums.append(int(input("두 번째 숫자를 입력하세요 : ")))
      # nums.append(int(nums[0] / nums[1]))
      print("{0} / {1} = {2}".format(nums[0], nums[1], nums[2]))
  except ValueError:
      print("오류 발생! 잘못된 값을 입력했습니다.")
  except ZeroDivisionError as err:
      print(err)
```

<br>

> 실행결과
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 3
  Traceback (most recent call last):
    File "c:\PythonWorkspace\ch10.py", line 7, in <module>
      print("{0} / {1} = {2}".format(nums[0], nums[1], nums[2]))
  IndexError: list index out of range
```
- IndexError : 리스트의 인덱스 범위를 벗어남

  - 현재 리스트에는 입력받은 두 수([6, 3])만 들어 있어서 인덱스는 0, 1 존재
 
  - format() 함수로 nums[2]에 접근하려고 해서 발생하는 오류

- IndexError 구문을 추가하면 예외 처리 가능

  - 모든 오류에 대한 예외 처리를 프로그램 안에 작성하려면 코드가 한없이 길어짐

<br>

> 지금까지 정의하지 않은 모든 오류를 예외 처리
```
  try:
      print("나누기 전용 계산기입니다.")
      nums = []
      nums.append(int(input("첫 번째 숫자를 입력하세요 : ")))
      nums.append(int(input("두 번째 숫자를 입력하세요 : ")))
      # nums.append(int(nums[0] / nums[1]))
      print("{0} / {1} = {2}".format(nums[0], nums[1], nums[2]))
  except ValueError:
      print("오류 발생! 잘못된 값을 입력했습니다.")
  except ZeroDivisionError as err:
      print(err)
  except Exception as err:
      print("알 수 없는 오류가 발생했습니다.")
      print(err)
```
- 코드 마지막에 구문 추가

  - except Exception as err

<br>

> 실행결과
```
  나누기 전용 계산기입니다.
  첫 번째 숫자를 입력하세요 : 6
  두 번째 숫자를 입력하세요 : 3
  알 수 없는 오류가 발생했습니다.
  list index out of range
```

<br>

#### 📌 예외 처리 클래스
```
  ValueError, ZeroDivisionError, IndexError는 예외 처리를 위해 파이썬에 미리 정의되어 있는 클래스
  
  이외에도 변수명이 없을 때 발생하는 NameError, 문법 오류가 있을 때 발생하는 SyntaxError, 접근하려는 파일이 없을 때 발생하는 FileNotFoundError 등 다양한 클래스 有
  
  마지막에 사용한 Exception은 앞에 나온 예외 처리 클래스들의 부모 클래스
   
  
  예외 처리 클래스 모두 외울 필요 X
  
  오류가 발생할 수 있는 상황을 마주했을 때 적절한 예외 처리 진행
```

<br>

### 연습문제
#### ✏️ 1. 다음 중 예외 처리에 대한 설명으로 잘못된 것은?
```
  ① 오류가 발생했을 때 프로그램을 멈추지 않고 계속 수행할 수 있도록 처리한다.
  
  ② except 문은 try 문에서 오류가 발생했을 때 실행할 문장을 적는다.
  
  ③ except 문은 처리하려는 오류 종류에 따라 여러 번 정의할 수 있다.
  
  ④ try 문은 단독으로 사용할 수 있다.
```

<details>
  <summary>정답</summary>

<br>

> ④ try 문은 단독으로 사용할 수 있다.

</details>

<br>




