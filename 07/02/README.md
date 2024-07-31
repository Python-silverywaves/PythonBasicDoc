# 전달값과 반환값
- 함수의 3가지 요소 = 전달값, 동작, 반환값

- 위의 open_account() 함수는 전달값과 반환값이 없고 동작만 정의돼 있음
  - 전달값과 반환값은 함수의 구성 요소이지만, 필수 요소는 X

  - 전달값과 반환값이 있는 함수도 있고 없는 함수도 있음
 
<br>

> 전달값과 반환값이 있는 함수를 만드는 형식
```
  def 함수명(전달값1, 전달값2, ...):  # 함수명 옆에 있는 소괄호 안에 필요한 개수만큼 전달값 넣기
      # 함수 본문
      실행할 문장1
      실행할 문장2
      ...
      return 반환값1    # 동작 수행이 끝나면 return 문으로 함수를 호출한 위치에 값을 반환
```
- 전달값 : 함수를 사용하려고 호출할 때 함수에 전달하는 값
- 함수 본문 : 전달값들을 활용해 어떤 동작을 수행
- 반환값 : 반환하는 값(보통 1개지만, 여러 값을 반환해야 하는 경우에는 쉼표로 구분해 튜플 형태로 반환 가능)

<br>

###  📌 ex) 입금하기
- 입금을 처리하는 함수 생성
  - 예금을 뜻하는 deposit이라는 이름 사용 & 전달값 2개
    - 첫 번째 전달값 = 현재 잔액을 의미하는 balance
    - 두 번째 전달값 = 입금하려는 금액을 의미하는 money

  - 함수 본문 : 동작으로 입금 완료를 안내하는 문구와 입금 후 잔액을 출력하는 내용 작성
    - 입금 후 잔액 = 현재 잔액 + 입금액

  - 마지막에 입금 후 잔액 정보를 반환하는 return 문 작성

<br>

> 함수 정의
```
  def open_account():
      print("새로운 계좌를 개설합니다.")
  
  open_account()                 # open_account() 함수 호출
   
  def deposit(balance, money):   # 입금 처리 함수
      print("{0}원을 입금했습니다. 잔액은 {1}원입니다.".format(money, balance + money))
      return balance + money     # 입금 후 잔액 정보 반환
```

<br>

- 함수를 호출해서 입금하기
  - 현재 잔액을 담는 변수 balance를 정의
    - 입금 내역이 없으니 초깃값은 0으로 저장
  - deposit() 함수를 호출하여 현재 잔액이 담긴 balance 변수와 입금할 금액인 1000을 넣어 전달
    - 현재 잔액은 0이므로 0과 1000, 2개의 값을 전달
  - deposit() 함수는 전달값을 받아 동작을 수행하고 값을 반환
    - 이 값을 받아 다시 balance 변수에 저장

<br>

> 함수 호출
```
  def open_account():
      print("새로운 계좌를 개설합니다.")
  
  open_account()                 # open_account() 함수 호출
  
  def deposit(balance, money):   # 입금 처리 함수
      print("{0}원을 입금했습니다. 잔액은 {1}원입니다.".format(money, balance + money))
      return balance + money     # 입금 후 잔액 반환
   
  
  balance = 0                     # 초기 잔액
  balance = deposit(balance, 1000)   # 1,000원 입금
```

<br>

#### 💡 참고 : 매개변수(parameter, 파라미터)
- 함수를 정의할 때 전달값을 받는 balance, money와 같은 변수

> 함수 정의의 balance 변수 vs 함수를 호출하는 부분의 balance 변수
```
  두 변수는 이름은 같지만, 같은 변수가 아님
  
  함수 정의에 있는 balance
    = 전달값(여기서는 0)을 저장하는 새로운 변수
    = money 도 1000이라는 값을 저장하는 새로운 변수
    = 이 둘은 함수 안에서만 사용 가능

  함수를 호출하는 부분의 balance
    = 변수에 어떤 값을 저장할 때처럼 함수를 호출하고 나서 반환하는 값을 변수에 다시 저장
    = return 문으로 반환하는 값을 함수 밖에 정의한 balance 변수에 저장
    = 현재 잔액을 나타내는 변수인데, 1,000원을 입금해 잔액이 변경됐으므로 deposit() 함수의 반환값을 받아 저장
```

<br>

#### 💡 참고 : return문
- 함수에서 return 문을 실행하고 나면 값을 반환함과 동시에 함수를 빠져나감
  - return 문 밑에 어떤 코드가 있다면 이 부분은 실행 X
  - 반복문을 탈출하는 break 문의 작동 방식과 비슷

<br>

#### 💡 참고 : 만약 함수를 호출하고 반환값을 저장하지 않으면?
> 기존 방식
```
  balance = 0   # balance 변수에 초깃값으로 0 저장
  balance = deposit(balance, 1000)   # balance 변수에 deposit() 함수의 반환값을 다시 저장
```

> 반환값 저장X
```
  deposit(balance, 1000)
```
- 함수가 어떤 값을 반환하기는 하지만, 이 값을 받아서 저장한 곳이 없으므로 반환값을 사용할 수 없음
  - 함수가 반환하는 값을 사용하려면 반환값을 저장할 변수 명시 필수

<br>

###  📌 ex) 출금하기
- 출금을 처리하는 함수 생성
  - 출금을 뜻하는 withdraw로 이름 사용 & 전달값을 2개
    - 첫 번째 전달값 = 현재 잔액
    - 두 번째 전달값 = 출금하려는 금액

- 출금의 기본 조건 : 계좌의 잔액 ≧ 출금액
  - 함수 본문에서 현재 잔액과 출금액을 비교
  - 잔액이 출금액과 같거나 많은 경우와 그렇지 않은 경우로 나뉘므로 두 방향으로 분기(if-else 문 사용)
    - 잔액이 많으면
      - 출금 완료를 안내하는 문구와 출금 후 잔액을 출력하는 내용을 작성
      - 출금 후 잔액 = 현재 잔액 - 출금액
      - 마지막에 출금 후 잔액 정보를 반환하는 return 문을 작성
    - 잔액이 적으면(조건을 만족하지 않으면)
      - else 문으로 가서 출금 실패를 안내하고 기존 잔액을 반환

<br>

> 출금
```
  def open_account(): # 계좌 개설 함수
      print("새로운 계좌를 개설합니다.")
  
  open_account() # open_account() 함수 호출
  
  def deposit(balance, money): # 입금 처리 함수
      print("{0}원을 입금했습니다. 잔액은 {1}원입니다.".format(money, balance + money))
      return balance + money   # 입금 후 잔액 반환
   
  
  def withdraw(balance, money): # 출금 처리 함수
      if balance >= money:       # 잔액이 출금액보다 많으면
          print("{0}원을 출금했습니다. 잔액은 {1}원입니다.".format(money, balance - money))
          return balance - money   # 출금 후 잔액 반환
      else:
          print("잔액이 부족합니다. 잔액은 {0}원입니다.".format(balance))
          return balance           # 기존 잔액 반환
  balance = 0 # 초기 잔액
  balance = deposit(balance, 1000) # 1,000원 입금
  
  # 출금
  balance = withdraw(balance, 2000) # 2,000원 출금 시도
  balance = withdraw(balance, 500)  # 500원 출금 시도
```

<details>
  <summary>실행 결과</summary>

<br>

```
  새로운 계좌를 개설합니다.
  1000원을 입금했습니다. 잔액은 1000원입니다.
  잔액이 부족합니다. 잔액은 1000원입니다.
  500원을 출금했습니다. 잔액은 500원입니다.
```
- 첫 번째 출금 시도
  - 출금액을 2,000원으로 전달
  - deposit() 함수를 호출한 후이므로 현재 잔액이 1,000원
  - 잔액이 출금하려는 금액보다 적으므로 출금하는 데 실패

- 두 번째 출금 시도
  - 출금액을 500원으로 전달
  - 잔액이 더 많아서 정상적으로 출금되고 출금 후 잔액도 반환

  
</details>

<br>

###  📌 ex) 수수료 부과하기
- 은행의 업무 시간이 아닐 때 출금(항상 잔액보다는 적은 금액을 출금하고, 업무시간 외 출금 수수료는 100원으로 가정)
  - 잔액과 수수료를 함께 반환

> 수수료 부과
```
  def open_account(): # 계좌 개설 함수
      print("새로운 계좌를 개설합니다.")
  
  open_account() # open_account() 함수 호출
  
  def deposit(balance, money): # 입금 처리 함수
      print("{0}원을 입금했습니다. 잔액은 {1}원입니다.".format(money, balance + money))
      return balance + money # 입금 후 잔액 반환
   
  
  def withdraw_night(balance, money): # 업무 시간 외 출금
      commission = 100 # 출금 수수료 100원
      print("업무 시간 외에 {}원을 출금했습니다.".format(money))
      return commission, balance - money - commission
   
  
  balance = 0 # 초기 잔액
  balance = deposit(balance, 1000) # 1,000원 입금
  
  # 업무 시간 외 출금 시도 : 튜플 형태로 반환한 값 2개를 각각 변수에 저장
  commission, balance = withdraw_night(balance, 500)
  print("수수료 {0}원이며, 잔액은 {1}원입니다.".format(commission, balance))
```

<details>
  <summary>실행결과</summary>

<br>

```
  새로운 계좌를 개설합니다.
  1000원을 입금했습니다. 잔액은 1000원입니다.
  업무 시간 외에 500원을 출금했습니다.
  수수료 100원이며, 잔액은 400원입니다.
```
- 1,000원을 입금한 상태에서 500원 출금
  - 업무 시간 외 수수료 100원을 제외한 400원이 잔액으로 표시
- return 문
  - 수수료(commission)와 기존 잔액에서 출금액과 수수료를 뺀 금액(balance - money - commission)을 쉼표로 구분해 함께 반환
  - commission과 balance 변수에 각각 수수료와 출금 후 잔액 정보를 저장

</details>

<br>

<details>
  <summary>튜플</summary>

<br>

> 쉼표로 구분해 값을 여러 개 적으면 함수를 호출하는 쪽에서도 한 번에 여러 값을 변수에 저장 가능
```
  (name, age, hobby) = ("피글렛", 20, "코딩")   # 변수명에 소괄호가 없어도 실행결과는 동일
  print(name, age, hobby)
```
```
  name, age, hobby = ("피글렛", 20, "코딩")   # 변수명에 소괄호가 없어도 실행결과는 동일
  print(name, age, hobby)
```
```
  name, age, hobby = "피글렛", 20, "코딩"     # 값에 소괄호가 없어도 실행결과는 동일
  print(name, age, hobby)
```

> 실행결과
```
  피글렛 20 코딩
```

</details>

<br>

#### 💡 참고 : 들여쓰기와 띄어쓰기
- 가독성 : 읽기 쉽도록 코드를 작성
  - 파이썬 코드 스타일 가이드(style guide) : [PEP 8](https://peps.python.org/pep-0008)
    - 다른 사람과 함께 작업할 때 또는 지금 작성하는 코드를 미래의 자신이 알아보기 쉽게 들여쓰기, 띄어쓰기 등 코드를 작성하는 방식을 통일

<br>

#### ✏️ 1. 다음 중 올바르게 설명한 사람을 모두 고른 것은?
|보기|
|-|
|수연 : 함수에는 전달값을 넣지 않아도 돼.<br>승민 : 함수에는 전달값을 마음껏 넣을 수 있어.<br>지안 : 전달값은 함수 밖에서도 얼마든지 사용할 수 있어.|

```
  ① 수연, 승민
  
  ② 승민, 지안
  
  ③ 수연, 지안
  
  ④ 수연, 승민, 지안
```

<details>
  <summary>정답</summary>

<br>

> ① 수연, 승민

</details>

<br>

#### ✏️ 2. 다음 조건에 해당하는 함수를 구현한 코드로 알맞은 것은?
|보기|
|-|
|A. 함수명은 add로 한다.<br>B. 수 2개를 num1, num2라는 이름으로 전달받는다.<br>C. num1과 num2를 서로 더한 값을 반환한다.|

```
  ①
  def add():
      return num1 + num2

  ②
  def add():
      throw num1 + num2

  ③
  def add(num1, num2):
      return num1 + num2

  ④
  def add(num1, num2):
      throw num1 + num2
```

<details>
  <summary>정답</summary>

<br>

>   ③
```
  def add(num1, num2):
      return num1 + num2
```

</details>

<br>
