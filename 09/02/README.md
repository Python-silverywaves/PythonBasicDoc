# 클래스와 객체 생성하기
|클래스는 붕어빵틀에 비유하곤 함|
|-|
|![image](https://github.com/user-attachments/assets/c18d5a25-9df5-4605-9dc1-3ee5d4e51b8b)|
|- 붕어빵을 만들 때 틀에다가 반죽과 속재료를 넣고 불에 구우면 똑같은 모양의 붕어빵을 여러 개 제작 가능<br>- 해당 틀로 만든 붕어빵은 반죽과 속재료를 바꿔도 항상 같은 모양<br>- 붕어빵 틀이 없다면 붕어빵을 하나씩 손으로 빚어야 함|

<br>

> 기본 형식
```
  class 클래스명:    # 클래스를 나타내는 class 키워드 뒤에 클래스명을 적고 콜론
      def 메서드명1(self, 전달값1, 전달값2, ...):  # 클래스에 속한 내용임을 표시하기 위해 들여쓰기 후 필요한 함수 정의
          실행할 명령1    # 메서드의 각 명령문은 메서드 소속임을 표시하기 위해 들여쓰기
          실행할 명령2
          ...
  
      def 메서드명2(self, 전달값1, 전달값2, ...):
          실행할 명령1
          실행할 명령2
          ...
```
- 클래스명 : 하나 또는 여러 단어의 조합으로 작명 & 각 단어의 첫 글자는 대문자
- 메서드(method)
  - 클래스 안에 정의하는 함수
  - 함수과 개념은 비슷하지만 첫 번째 전달값 위치에 self 넣는다는 점이 다름

<br>

<details>
  <summary>self</summary>

<br>

> self
```
  객체인 자기 자신을 의미
  
  생성자 또는 메서드에서 self를 전달값에 넣는다 = 객체를 받는다
  
  메서드 안에서 self.을 사용하는 것은 객체의 인스턴스 변수 또는 메서드에 접근하겠다는 의미
```

<br>

> flamethrower1
```
  AttackUnit 클래스의 인스턴스
  
  flamethrower1 객체를 생성할 때는 name, hp, damage 정보만 전달하지만,
  자동으로 호출되는 __init__() 생성자의 첫 번째 전달값에 있는 self에 flamethrower1 객체도 전달한다
  
  생성자 안에 작성한 self.name = name은 flamethrower1.name = name과 같은 의미
```

<br>

- 클래스의 메서드는 첫 번째 전달값이 self
- 클래스 안에서는 변수 또는 메서드에 접근하려면 self.name 또는 self.attack(...)처럼 인스턴스 변수 또는 메서드명 앞에 self.을 함께 기재

</details>

<br>


### 유닛 생성 코드를 클래스 사용하여 재작성
- 클래스명은 Unit으로 정의
- Unit 클래스 안에 메서드 __init__(언더바를 앞뒤로 각각 2개씩) 정의
  - 첫 번째 전달값 : self
  - 나머지 전달값 : 이름, 체력, 공격력
  - 메서드 안에는 전달값을 받는 변수를 정의 ← 인스턴스 변수
- 생성한 유닛 정보를 print() 문으로 출력

<br>

> 변수 정의 형식
```
  self.변수명 = 값
```

<br>

<details>
  <summary>인스턴스 변수</summary>

```
  - 메서드 안에 정의한 변수
  - 클래스 안에서 사용하는 변수
```

</details>

<br>

> 적용 코드
```
  class Unit:
      def __init__(self, name, hp, damage):
          self.name = name     # 인스턴스 변수 name에 전달값 name 저장
          self.hp = hp         # 인스턴스 변수 hp에 전달값 hp 저장
          self.damage = damage # 인스턴스 변수 damage에 전달값 damage 저장
          print("{0} 유닛을 생성했습니다.".format(self.name))
          print("체력 {0}, 공격력 {1}".format(self.hp, self.damage))
```
- 클래스도 함수와 마찬가지로 정의만 해서는 아무런 동작 X
  - 지금은 붕어빵 틀만 불에 올려 달군 상태

### 클래스를 사용해 유닛 생성
> 형식
```
  객체명 = 클래스명(전달값1, 전달값2, ...) # self를 제외한 나머지 전달값
```

<br>

> 적용 코드
```
  class Unit:
      def __init__(self, name, hp, damage):
          self.name = name     # 인스턴스 변수 name에 전달값 name 저장
          self.hp = hp         # 인스턴스 변수 hp에 전달값 hp 저장
          self.damage = damage # 인스턴스 변수 damage에 전달값 damage 저장
          print("{0} 유닛을 생성했습니다.".format(self.name))
          print("체력 {0}, 공격력 {1}".format(self.hp, self.damage))
   
  # 소괄호 안에는 클래스의 __init__() 메서드에 정의한 부분 중 self를 제외한 나머지 전달값(name, hp, damage) 넣기
  soldier1 = Unit("보병", 40, 5) # 보병1 생성, 전달값으로 이름/체력/공격력 전달
  soldier2 = Unit("보병", 40, 5) # 보병2 생성, 전달값으로 이름/체력/공격력 전달
  tank = Unit("탱크", 150, 35) # 탱크 생성, 전달값으로 이름/체력/공격력 전달
```

<br>

> 실행결과 : 클래스 하나로 서로 다른 유닛 3개 생성
```
  보병 유닛을 생성했습니다.
  체력 40, 공격력 5
  보병 유닛을 생성했습니다.
  체력 40, 공격력 5
  탱크 유닛을 생성했습니다.
  체력 150, 공격력 35
```

<br>

### 인스턴스와 객체
- 객체(object)
  - 클래스로 만들어진 유닛들
    - 붕어빵
    - soldier1, soldier2, tank
- 클래스의 인스턴스(instance)
  - 객체
    - 붕어빵은 붕어빵 틀의 인스턴스
    - soldier1, soldier2, tank 객체는 Unit 클래스의 인스턴스

<br>

|객체와 인스턴스는 사실 같은 개념|
|-|
|![image](https://github.com/user-attachments/assets/342fa39f-24c3-4272-a9b4-35b1897bfde8)|
|- 객체를 만드는 것 = 클래스의 인스턴스를 만드는 것<br>- 보통 객체를 단독으로 부를 때는 객체, 클래스와 연결지어 부를 때는 인스턴스로 표현|

<br>

#### 📌 정리
> 클래스
```
  서로 관련 있는 변수(인스턴스 변수)와 함수(메서드)들의 집합

  게임에서 보병과 탱크는 모두 이름, 체력, 공격력이 있는데, 이는 유닛들의 공통 속성이므로 하나의 틀(클래스)로 정의 가능
    - 클래스 안에는 메서드를 여러 개 정의 가능
    - 각 메서드의 첫 번째 전달값 위치에는 self
    - __init__() 메서드는 클래스에 필요한 값을 전달받아 self로 클래스의 인스턴스 변수를 정의
```

<br>

생성자(constructor) : __init__( )
---
- 사용자가 따로 호출하지 않아도 객체를 생성할 때 자동으로 호출되는 메서드
  - 클래스를 만들 때 __init__이라는 이름으로 메서드를 정의하면 자동으로 생성자가 됨

- 객체를 생성할 때 생성자가 자동으로 호출되므로 생성자의 전달값 개수만큼 값을 전달해야 함
  - self는 기본으로 포함하므로 제외

- 클래스에 따로 생성자를 정의하지 않았다면 전달값 없이 클래스명만으로 객체 생성

> 형식
```
  변수명 = 클래스명()
```

<br>

#### 💡 전달값을 다르게 주면?
> Unit 클래스
```
  class Unit:
      def __init__(self, name, hp, damage): # 생성자, self 외 전달값 3개(name, hp, damage)
          self.name = name
          self.hp = hp
          self.damage = damage
          print("{0} 유닛을 생성했습니다.".format(self.name))
          print("체력 {0}, 공격력 {1}".format(self.hp, self.damage))

  # 유닛(객체) 생성할 때 값을 3개씩 전달
  soldier1 = Unit("보병", 40, 5) # 객체 생성
  soldier2 = Unit("보병", 40, 5) # 객체 생성
  tank = Unit("탱크", 150, 35) # 객체 생성
```

<br>

> 만약 전달값을 3개가 아닌 1개만 넘기면??
```
  soldier3 = Unit("보병") # 전달값 3개 중 1개만 넘김
```

> 실행결과 : 오류 발생
```
  TypeError: __init__() missing 2 required positional arguments: 'hp' and 'damage'
```

<br>

> 만약 전달값을 3개가 아닌 2개만 넘기면??
```
  soldier3 = Unit("보병", 40) # 전달값 3개 중 2개만 넘김
```

> 실행결과 : 오류 발생
```
  TypeError: __init__() missing 1 required positional argument: 'damage'
```

<br>

인스턴스 변수
---
- 클래스의 메서드에서 정의하거나 객체를 통해 직접 정의
  - 클래스로부터 객체를 만든 다음, 객체만을 위한 인스턴스 변수가 필요한 경우에는 클래스 외부에서 별도로 정의 가능
    - 해당 객체를 제외한 다른 객체들은 새로 정의한 인스턴스 변수를 알지 못하며 사용 불가
    - 오직 한 객체만을 위한 인스턴스 변수
- self와 함께 사용
- Unit 클래스에서는 name, hp, damage가 인스턴스 변수, self.name과 같은 형식으로 전달값을 받아 정의

<br>

### 전투기 유닛 생성
- 공중을 날아다니는 유닛
- 은폐라는 특수한 기능이 있어서 이 기능을 쓰면 상대방이 볼 수 없음
  - 은폐는 그냥 쓸 수 없고 게임에서 통용되는 재화를 지불해서 업그레이드해야 사용 가능

<br>

> 적용 코드
```
  class Unit:
      def __init__(self, name, hp, damage): # 생성자, self 외 전달값 3개
          # 클래스 안에서는 self.으로 인스턴스 변수에 접근 가능
          self.name = name     # 인스턴스 변수 name
          self.hp = hp         # 인스턴스 변수 hp
          self.damage = damage # 인스턴스 변수 damage
          print("{0} 유닛을 생성했습니다.".format(self.name))
          print("체력 {0}, 공격력 {1}".format(self.hp, self.damage))

  # 전투기: 공중 유닛, 은폐 불가
  stealth1 = Unit("전투기", 80, 5) # 객체 생성, 체력 80, 공격력 5
  # 클래스 밖에서는 객체로 인스턴스 변수에 접근 가능
  print("유닛 이름 : {0}, 공격력 : {1}".format(stealth1.name, stealth1.damage))  # 객체명 뒤에 점(.)을 찍고 인스턴스 변수명 기재
```

<br>

> 실행결과
```
  전투기 유닛을 생성했습니다.
  체력 80, 공격력 5
  유닛 이름 : 전투기, 공격력 : 5  
```

<br>

### 전투기 유닛 추가 생성
- 객체명 : stealth2
  - 은폐 기능까지 업그레이드했다고 가정
- Unit 클래스의 인스턴스 변수에는 name, hp, damage만 있어서 은폐 상태 관리 불가
  - 업그레이드한 전투기만을 위한 특별한 인스턴스 변수를 하나 정의
    - 변수 이름 : cloaking
    - True일 때는 은폐 상태, False일 때는 일반 상태
- 은폐 상태가 잘 설정됐는지 확인
  - cloaking 변수의 값이 True이므로 if 문으로 값이 True인지 확인

<br>

> 적용코드
```
  # 은폐 가능
  stealth2 = Unit("업그레이드한 전투기", 80, 5)

  # 업그레이드한 전투기만을 위한 특별한 인스턴스 변수 정의, 은폐 상태
  stealth2.cloaking = True

  if stealth2.cloaking == True: # 은폐 상태라면
    print("{0}는 현재 은폐 상태입니다.".format(stealth2.name))
```

<br>

> 실행코드
```
  업그레이드한 전투기는 현재 은폐 상태입니다.
```
- 클래스 외부에서 직접 cloaking이라는 인스턴스 변수를 정의
  - Unit 클래스의 모든 객체가 아닌 오직 stealth2에만 해당하는 인스턴스 변수
  - stealth2.cloaking으로 접근해 값을 비교 가능

<br>

> 다른 전투기의 은폐 여부 확인
```
  if stealth1.cloaking == True: # 다른 전투기의 은폐 여부
      print("{0}는 현재 은폐 상태입니다.".format(stealth1.name))
```

<br>

> 실행결과
```
  AttributeError: 'Unit' object has no attribute 'cloaking'
```
- Unit 클래스에는 처음과 변함없이 name, hp, damage라는 3개의 인스턴스 변수만 있고 cloaking은 없음
  - stealth1에서 클래스에 정의하지 않은 cloaking 변수에 접근하니 오류 발생

<br>

#### 💡 두 객체의 인스턴스 변수 비교

|stealth1의 인스턴스 변수|stealth2의 인스턴스 변수|
|-|-|
|name|name|
|hp|hp|
|damage|damage|
|-|cloaking|

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  class Unit:
      def __init__(self, name, hp, damage): # 생성자, self 외 전달값 3개
          self.name = name     # 인스턴스 변수 name
          self.hp = hp         # 인스턴스 변수 hp
          self.damage = damage # 인스턴스 변수 damage
          print("{0} 유닛을 생성했습니다.".format(self.name))
          print("체력 {0}, 공격력 {1}".format(self.hp, self.damage))
  
  # 전투기: 공중 유닛, 은폐 불가
  stealth1 = Unit("전투기", 80, 5) # 체력 80, 공격력 5
  # 인스턴스 변수 접근
  print("유닛 이름 : {0}, 공격력 : {1}".format(stealth1.name, stealth1.damage))
  
  # 은폐 가능
  stealth2 = Unit("업그레이드한 전투기", 80, 5)
  # 업그레이드한 전투기만을 위한 특별한 인스턴스 변수 정의, 은폐 상태
  stealth2.cloaking = True
  
  if stealth2.cloaking == True: # 은폐 상태라면
      print("{0}는 현재 은폐 상태입니다.".format(stealth2.name))
  
  # 오류 발생
  # if stealth1.cloaking == True: # 다른 전투기의 은폐 여부
  #    print("{0}는 현재 은폐 상태입니다.".format(stealth1.name))
```

</details>

<br>

메서드
---
- 클래스 내부에 정의한 함수
  - 클래스 안에 여러 개 생성 가능
- 일반 함수와 다른 점
  - 전달값 부분에 첫 번째로 self를 넣는다는 점
  - 메서드 안에서 self.으로 인스턴스 변수에 접근할 수 있다는 점

<br>

### 공격할 수 있는 유닛만을 위한 새로운 클래스를 정의
- 이름 : AttackUnit
  - Unit 클래스와 동일하게 __init__() 생성자에서 name, hp, damage 인스턴스 변수를 정의
  - print() 문으로 출력하는 내용 X
- 공격 명령을 내리면 공격하는 동작, 적군으로부터 공격받으면 피해를 입는 동작 등을 정의
  - 공격 동작
    - 메서드명 : attack
    - 전달값 : 기본적으로 넣어야 하는 self + 공격 방향을 의미하는 location
    - 공격 명령을 받아 적군을 공격하러 갈 때는 공격하러 갈 유닛의 이름과 공격 방향 정보, 공격력을 출력
      - 유닛의 이름과 공격력은 클래스의 생성자에 인스턴스 변수로 이미 정의돼 있으므로 self.으로 접근해 사용
      - 공격 방향은 명령을 받을 때마다 달라질 수 있으므로 인스턴스 변수가 아닌 전달값을 그대로 사용(self. 없이 사용)
  - 공격받아 피해를 입는 동작
    - 메서드명 : damaged
    - 전달값 : 피해량(적군의 공격 유닛은 종류별로 공격력이 다르고 상황에 따라 피해 규모가 달라질 수 있음)을 의미하는 damage
    - 유닛의 현재 체력 정보에서 damage의 값만큼 빼서 남은 체력 확인
      - 공격받은 후 남은 체력이 0 이하라면 유닛을 사용할 수 없으므로 유닛을 파괴 처리

<br>

> 적용 코드
```
  class AttackUnit: # 공격 유닛
      def __init__(self, name, hp, damage):
          self.name = name
          self.hp = hp
          self.damage = damage

      def attack(self, location): # 전달받은 방향으로 공격
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage)) # 공간이 좁아서 2줄로 나눔

      def damaged(self, damage): # damage만큼 유닛 피해
          # 피해 정보 출력
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage # 유닛의 체력에서 전달받은 damage만큼 감소

          # 남은 체력 출력
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0: # 남은 체력이 0 이하이면
              print("{0} : 파괴됐습니다.".format(self.name)) # 유닛 파괴 처리
```

<br>

<details>
  <summary>코드 줄바꿈</summary>

<br>

> 코드를 작성할 때 문장이 너무 길어서 한 줄로 표현하기 어렵거나 보기 좋게 두 줄 이상으로 나눠 적으려면 나누려는 부분에 역슬래시(\)를 넣고 줄 바꿈
>> 그러면 실행했을 때 한 문장으로 인식
```
      def attack(self, location): # 전달받은 방향으로 공격
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage)) # 공간이 좁아서 2줄로 나눔
```

</details>

<br>

### AttackUnit 클래스의 객체를 만들어 작성한 메서드 사용
### 화염방사병 유닛 생성
- 보병과 비슷한 공격 유닛
  - 화염방사기를 다루며 보병의 총보다 사정거리는 짧지만 가까운 거리에 있는 적에게는 가공할 만한 위력 행사

<br>

> 적용 코드
```
  # 화염방사병: 공격 유닛, 화염방사기를 사용함
  flamethrower1 = AttackUnit("화염방사병", 50, 16) # 객체 생성, 체력 50, 공격력 16
  flamethrower1.attack("5시") # 5시 방향으로 공격 명령
```

<br>

> 실행결과
```
  화염방사병 : 5시 방향 적군을 공격합니다. [공격력 16]
```

<br>

> 공격하는 와중에 적군으로부터 피해를 입는다고 가정하고 25만큼의 피해를 2번 받도록 코드 작성
```
  # 25만큼의 공격을 2번 받음
  flamethrower1.damaged(25) # 남은 체력 25
  flamethrower1.damaged(25) # 남은 체력 0
```

<br>

> 실행결과
```
  화염방사병 : 25만큼 피해를 입었습니다.
  화염방사병 : 현재 체력은 25입니다.
  화염방사병 : 25만큼 피해를 입었습니다.
  화염방사병 : 현재 체력은 0입니다.
  화염방사병 : 파괴됐습니다.
```

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  class AttackUnit: # 공격 유닛
      def __init__(self, name, hp, damage):
          self.name = name
          self.hp = hp
          self.damage = damage
  
      def attack(self, location): # 전달받은 방향으로 공격
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage)) # 공간이 좁아서 2줄로 나눔
  
      def damaged(self, damage): # damage만큼 유닛 피해
          # 피해 정보 출력
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage # 유닛의 체력에서 전달받은 damage만큼 감소
          # 남은 체력 출력
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0: # 남은 체력이 0 이하이면
              print("{0} : 파괴됐습니다.".format(self.name)) # 유닛 파괴 처리
  
  # 화염방사병: 공격 유닛, 화염방사기를 사용함
  flamethrower1 = AttackUnit("화염방사병", 50, 16) # 객체 생성, 체력 50, 공격력 16
  flamethrower1.attack("5시") # 5시 방향으로 공격 명령
  
  # 25만큼의 공격을 2번 받음
  flamethrower1.damaged(25) # 남은 체력 25
  flamethrower1.damaged(25) # 남은 체력 0
```

</details>

<br>

#### ✏️ 1. 다음 [가]에 들어갈 용어로 알맞은 것은?
|보기|
|-|
|A 클래스로부터 만들어진 객체 B가 있다고 할 때, B는 A의 [가]라고 표현한다.|

```
  ① 인스턴트
  
  ② 인스턴스
  
  ③ 오브젝트
  
  ④ 블루프린트
```

<details>
  <summary>정답</summary>

<br>

> ② 인스턴스

</details>

<br>

#### ✏️ 2. 다음 클래스 객체의 name 변수에 값을 저장하기 위해 [가]에 들어갈 기호로 알맞은 것은?
```
  class Student:
      (생략)
  
  student = Student()
  student[가]name = "나학생"
```

```
  ① .
  
  ② ,
  
  ③ :
  
  ④ ->
```

<details>
  <summary>정답</summary>

<br>

> ① .

</details>

<br>

#### ✏️ 3. 다음 중 클래스에 관한 설명으로 잘못된 것은?
```
  ① __init__() 함수 내에서 self.name = name과 같이 정의되는 변수를 인스턴스 변수라고 한다.
  
  ② 특정 객체에 변수를 따로 추가하면 해당 클래스로 만든 모든 객체에 동일하게 변수가 추가된다.
  
  ③ 서로 다른 두 객체의 인스턴스 변수는 서로 다른 값을 가질 수 있다.
  
  ④ 인스턴스 변수는 없을 수도 있고 여러 개가 있을 수도 있다.
```

<details>
  <summary>정답</summary>

<br>

> ② 특정 객체에 변수를 따로 추가하면 해당 클래스로 만든 모든 객체에 동일하게 변수가 추가된다.
```
  객체만을 위한 인스턴스 변수가 필요한 경우에 객체에서 직접 정의 가능
  이때 해당 객체를 제외한 나머지 객체는 새로 정의한 인스턴스 변수를 알지 못하고 사용할 수도 없음
```

</details>

<br>
