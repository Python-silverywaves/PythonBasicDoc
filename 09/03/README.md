# 클래스 상속하기
### 상속(inheritance)
- 자식이 부모로부터 재산을 물려받는 것
- 한 클래스의 내용을 다른 클래스가 물려받아 사용하는 것
- 다른 클래스로부터 상속받을 때는 클래스명 뒤에 소괄호를 적고 상속받을 클래스명을 명시
  - 두 클래스는 실생활에서 자식이 부모로부터 상속받는 관계와 비슷해서 자식 클래스와 부모 클래스라고 표현

<br>

> 형식
```
  class 자식 클래스(부모 클래스):
```

<br>

### 상속이란
- 유닛 중에서 공격할 수 없는 유닛
  - 유닛들의 수송을 담당하는 수송선, 부상당한 유닛을 치료해 주는 의무병 등
  - 공격 명령이 포함된 AttackUnit 클래스로 생성 불가
- damage 인스턴스 변수를 포함해 공격과 관련한 내용은 AttackUnit 클래스에 있으므로 Unit 클래스는 일반적인 유닛을 위한 클래스로 수정
  - 모든 유닛은 이름과 체력 정보가 있어야 하므로 name, hp 인스턴스 변수는 유지
  - 공격력인 damage 인스턴스 변수 삭제
  - 코드를 간결하게 하기 위해 print() 문도 삭제

<br>

> 수정 전
```
  class Unit:
      def __init__(self, name, hp, damage): # 공격력인 damage 삭제
          self.name = name
          self.hp = hp
          self.damage = damage # 삭제
          print("{0} 유닛을 생성했습니다.".format(self.name)) # 삭제
          print("체력 {0}, 공격력 {1}".format(self.hp, self.damage)) # 삭제
```

<br>

> 수정 후
```
  # 일반 유닛
  class Unit:
      def __init__(self, name, hp):
          self.name = name
          self.hp = hp
```

<br>

> AttackUnit 클래스
```
  # 공격 유닛
  class AttackUnit:
      def __init__(self, name, hp, damage):
          self.name = name # 공통 부분
          self.hp = hp # 공통 부분
          self.damage = damage
      (생략)
```
- __init__() 생성자 부분만 보면 Unit 클래스와 AttackUnit 클래스의 공통 부분 존재
  - 유닛의 특성에 따라 공격 유닛, 공중 유닛, 지상 유닛 등으로 확장된다면 클래스마다 name, hp 인스턴스 변수를 일일이 넣어야 함
  - 이때 상속을 통해 클래스에 공통되는 부분을 중복으로 작성하지 않고 재사용 가능
- AttackUnit 클래스는 Unit 클래스의 name, hp 인스턴스 변수를 포함하면서 추가로 damage 인스턴스 변수를 정의
  - Unit 클래스로부터 상속받으면 Unit 클래스의 name, hp 인스턴스 변수를 정의하지 않아도 그대로 사용 가능

<br>

> AttackUnit 클래스의 코드 간소화(상속)
```
  # 공격 유닛
  class AttackUnit(Unit): # Unit 클래스 상속
      def __init__(self, name, hp, damage):  # self도 함께 넘겨 줘야 함
          Unit.__init__(self, name, hp) # 부모 클래스의 생성자 호출
          self.damage = damage
      (생략)
```
- AttackUnit 클래스는 Unit 클래스의 모든 인스턴스 변수와 메서드를 그대로 사용 가능
- AttackUnit 클래스만을 위한 인스턴스 변수와 메서드 추가 가능

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  # 일반 유닛
  class Unit:
      def __init__(self, name, hp):
          self.name = name
          self.hp = hp
  
  # 공격 유닛
  class AttackUnit(Unit): # Unit 클래스 상속
      def __init__(self, name, hp, damage):
          Unit.__init__(self, name, hp) # 부모 클래스의 생성자 호출
          self.damage = damage
  
      def attack(self, location): # 전달받은 방향으로 공격
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage))
  
      def damaged(self, damage): # damage만큼 유닛 피해
          # 피해 정보 출력
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage # 유닛의 체력에서 전달받은 damage만큼 감소
          # 남은 체력 출력
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0: # 남은 체력이 0 이하이면
              print("{0} : 파괴됐습니다.".format(self.name)) # 유닛 파괴 처리

  flamethrower1 = AttackUnit("화염방사병", 50, 16)
  flamethrower1.attack("5시") # 5시 방향으로 공격 명령
  
  # 25만큼의 공격을 2번 받음
  flamethrower1.damaged(25) # 남은 체력 25
  flamethrower1.damaged(25) # 남은 체력 0
```

<br>

> 실행결과
```
  화염방사병 : 5시 방향 적군을 공격합니다. [공격력 16]
  화염방사병 : 25만큼 피해를 입었습니다.
  화염방사병 : 현재 체력은 25입니다.
  화염방사병 : 25만큼 피해를 입었습니다.
  화염방사병 : 현재 체력은 0입니다.
  화염방사병 : 파괴됐습니다.
```
- Unit 클래스 간소화 & AttackUnit 클래스는 Unit 클래스를 상속하도록 변경
  - AttackUnit 클래스는 부모 클래스로부터 상속받은 hp, name 인스턴스 변수를 그대로 사용

</details>

<br>

### 상속 사용 이유
- 서로 관련 있는 클래스들에서 공통 부분을 모아 부모 클래스로 정의하고 자식 클래스에서는 필요한 부분을 확장해 사용
  - 불필요한 코드의 중복 작성 방지
  - 수정이나 추가 사항이 생길 때 작업 범위 최소화

<br>

### 다중 상속(multiple inheritance)
- 클래스를 2개 이상 상속받는 것

<br>

> 형식
```
  class 자식 클래스(부모 클래스1, 부모 클래스2, ...):
```

<br>

#### 예시
- 공중 유닛
  - 전투기와 같이 공격이 가능한 유닛 or 보병, 탱크 등 지상 유닛을 다른 위치로 수송하면서 공격력은 없는 수송선 같은 유닛
  - 날 수 있기때문에 이 기능은 지상 유닛에는 적용 X
  - 무게나 크기, 종류, 비행 속도 업그레이드 여부에 따라 비행 속도 상이함
- 비행 기능을 정의하는 클래스 별도 생성
  - 클래스명 : Flyable
    - Flyable 클래스는 비행 기능만 제공하므로 어떤 유닛인지에 대한 정보는 포함 X
  - 인스턴스 변수 : 비행할 때 속도를 의미하는 flying_speed
  - 비행 동작은 fly() 메서드로 정의
    - fly() 메서드를 호출할 때 유닛의 이름과 비행 방향 정보를 전달 받음

<br>

> 적용 코드
```
  # 비행 기능
  class Flyable:
      def __init__(self, flying_speed): # 비행 속도
          self.flying_speed = flying_speed
  
      def fly(self, name, location): # 유닛 이름, 비행 방향
          print("{0} : {1} 방향으로 날아갑니다. [속도 {2}]" \
              .format(name, location, self.flying_speed))
```

<br>

- 공중 공격 유닛
  - 전투기는 비행하며 공격할 수 있는 공중 공격 유닛
  - '공격’ 유닛인 AttackUnit 클래스와 ‘공중’(비행 기능)을 제공하는 Flyable 클래스를 조합하면 공중 공격 유닛
- 공중 공격 유닛을 위한 새로운 클래스 생성
  - 클래스명 : FlyableAttackUnit
  - AttackUnit 클래스와 Flyable 클래스를 함께 상속(다중 상속)

<br>

> __init__() 생성자 안에서 상속받은 클래스들의 __init__() 생성자를 각각 호출
```
  # 공중 공격 유닛
  class FlyableAttackUnit(AttackUnit, Flyable):
      # 유닛 이름, 체력, 공격력, 비행 속도
      def __init__(self, name, hp, damage, flying_speed):
          AttackUnit.__init__(self, name, hp, damage) # 유닛 이름, 체력, 공격력
          Flyable.__init__(self, flying_speed) # 비행 속도
```

<br>

- 요격기 유닛 생성
  - 미사일 여러 발을 한 번에 발사하는 공중 공격 유닛
  - 혼자 있을 때보다 여럿이 모였을 때 적군에게 더 강력한 피해를 입힘
- FlyableAttackUnit 클래스로 새로운 객체를 만들고 이름은 interceptor
  - 생성자에는 유닛 이름, 체력, 공격력, 비행 속도 정보를 전달
  - Flyable 클래스에 정의한 fly() 메서드를 호출
    - 이동할 유닛 이름과 방향 정보를 전달값으로 넘김

<br>

> 적용 코드
```
  # 요격기: 공중 공격 유닛, 미사일 여러 발을 한 번에 발사
  # 유닛 이름, 체력, 공격력, 비행 속도
  interceptor = FlyableAttackUnit("요격기", 200, 6, 5)
  interceptor.fly(interceptor.name, "3시") # 3시 방향으로 이동
```

<br>

> 실행결과
```
  요격기 : 3시 방향으로 날아갑니다. [속도 5]
```

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  # 일반 유닛
  class Unit:
      def __init__(self, name, hp):
          self.name = name
          self.hp = hp
  
  # 공격 유닛
  class AttackUnit(Unit): # Unit 클래스 상속
      def __init__(self, name, hp, damage):
          Unit.__init__(self, name, hp) # 부모 클래스의 생성자 호출
          self.damage = damage
  
      def attack(self, location): # 전달받은 방향으로 공격
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage))
  
      def damaged(self, damage): # damage만큼 유닛 피해
          # 피해 정보 출력
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage # 유닛의 체력에서 전달받은 damage만큼 감소
          # 남은 체력 출력
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0: # 남은 체력이 0 이하이면
              print("{0} : 파괴됐습니다.".format(self.name)) # 유닛 파괴 처리
  
  # 비행 기능
  class Flyable:
      def __init__(self, flying_speed): # 비행 속도
          self.flying_speed = flying_speed
  
      def fly(self, name, location): # 유닛 이름, 비행 방향
          print("{0} : {1} 방향으로 날아갑니다. [속도 {2}]" \
              .format(name, location, self.flying_speed))
  
  # 공중 공격 유닛
  class FlyableAttackUnit(AttackUnit, Flyable):
      # 유닛 이름, 체력, 공격력, 비행 속도
      def __init__(self, name, hp, damage, flying_speed):
          AttackUnit.__init__(self, name, hp, damage) # 이름, 체력, 공격력
          Flyable.__init__(self, flying_speed) # 비행 속도
  
  # 요격기: 공중 공격 유닛, 미사일 여러 발을 한 번에 발사
  # 유닛 이름, 체력, 공격력, 비행 속도
  interceptor = FlyableAttackUnit("요격기", 200, 6, 5)
  interceptor.fly(interceptor.name, "3시") # 3시 방향으로 이동
```

</details>

<br>

#### 💡 클래스와 상속 관계
|-|
|-|
|![image](https://github.com/user-attachments/assets/2d881198-951c-483e-8c0c-5f44ebc75ffe)|
|- 모든 유닛에 공통 요소인 이름과 체력을 담은 일반 유닛 클래스 Unit<br>- Unit 클래스를 상속받아 공격력까지 표시하는 공격 유닛 클래스 AttackUnit 정의<br>- 비행 기능이 있는 Flyable 클래스 정의<br>- Flyable 클래스는 비행 속도 정보와 비행 동작 메서드만 보유<br>- 공중 공격 유닛을 위해 AttackUnit 클래스와 Flyable 클래스를 다중 상속하는 FlyableAttackUnit 클래스 생성<br>- FlyableAttackUnit 클래스는 전투기나 요격기를 만들기에 적합|

<br>

메서드 오버라이딩
---
- 상속 관계일 때 자식 클래스에서 부모 클래스에 정의한 메서드를 그대로 사용하지 않고 같은 이름으로 메서드를 새롭게 정의해 사용하는 방법

<br>

#### 예시
- 게임에서 유닛들은 플레이어가 지정한 위치나 방향으로 이동
  - 유닛마다 이동 속도 상이함
- 지상 유닛의 이동 속도를 의미하는 speed 인스턴스 변수를 Unit 클래스에 추가
- 이동 동작을 나타내는 move() 메서드를 정의하고 공중 유닛과 구분하는 문구를 추가해서 어떤 유닛이 몇 시 방향으로 이동하는지 출력

<br>

> 적용 코드
```
  # 일반 유닛
  class Unit:
      def __init__(self, name, hp, speed): # speed 추가
          self.name = name
          self.hp = hp
          self.speed = speed # 지상 이동 속도
   
  
      def move(self, location): # 이동 동작 정의
          print("[지상 유닛 이동]")
          print("{0} : {1} 방향으로 이동합니다. [속도 {2}]" \
              .format(self.name, location, self.speed))
```
- Unit 클래스를 변경하고 나면 Unit 클래스를 상속받는 자식 클래스에 영향 끼침
  - speed 인스턴스 변수를 새로 추가했으니 __init__() 생성자를 사용하는 부분은 변경

<br>

> AttackUnit 클래스
```
  # 공격 유닛
  class AttackUnit(Unit): # Unit 클래스 상속
      def __init__(self, name, hp, damage, speed): # speed 추가
          Unit.__init__(self, name, hp, speed) # speed 추가
          self.damage = damage
      (생략)
```

<br>

> AttackUnit 클래스를 상속받는 FlyableAttackUnit 클래스 수정
```
  # 공중 공격 유닛
  class FlyableAttackUnit(AttackUnit, Flyable):
      def __init__(self, name, hp, damage, flying_speed):
          AttackUnit.__init__(self, name, hp, damage, 0) # 지상 이동 속도 0(지상에서는 이동하지 못함)
          Flyable.__init__(self, flying_speed) # 비행 속도
```

<br>

#### 지상 이동 속도를 포함한 새로운 공격 유닛 생성
- 지상 유닛 중에서 가장 속도가 빠른 호버 바이크
  - AttackUnit 클래스로 호버 바이크 객체 생성
  - 전달값 : 지상 이동 속도 10, 체력 80, 공격력 20

<br>

> 적용 코드
```
  # 호버 바이크: 지상 유닛, 기동성 좋음
  hoverbike = AttackUnit("호버 바이크", 80, 20, 10) # 지상 이동 속도 10
```

<br>

#### 새로운 공중 공격 유닛 생성
- 우주 순양함
  - 유닛 중 가장 강력한 거대 함
  - 체력은 500, 공격력은 25, 비행 속도는 3

> 적용 코드
```
  # 우주 순양함: 공중 유닛, 체력도 굉장히 좋음, 공격력도 좋음
  spacecruiser = FlyableAttackUnit("우주 순양함", 500, 25, 3) # 비행 속도 3
```

<br>

> 두 유닛 이동
```
  hoverbike.move("11시")  # 지상 유닛이므로 move() 메서드로 이동
  spacecruiser.fly(spacecruiser.name, "9시")  # 공중 유닛이므로 fly() 메서드로 이동
```

<br>

> 실행결과
```
  [지상 유닛 이동]
  호버 바이크 : 11시 방향으로 이동합니다. [속도 10]
  우주 순양함 : 9시 방향으로 날아갑니다. [속도 3]
```
- 공중 공격 유닛인 우주 순양함이 지상 유닛 이동에 포함돼 보임
- 많은 유닛들을 이동할 때마다 지상 유닛인지 공중 유닛인지 구분해 move()와 fly() 메서드를 적용하는 것은 번거로움
- fly() 메서드를 사용할 때 유닛의 이름 정보까지 전달해야 하는 불편함

<br>

### Unit 클래스에 정의한 move() 메서드를 FlyableAttackUnit 클래스에서 오버라이딩
- 메서드 오버라이딩할 때는 부모 클래스에 정의한 메서드를 그대로 자식 클래스에서 동일한 이름과 전달값으로 정의하고, 메서드 동작만 원하는 대로 변경
- FlyableAttackUnit 클래스가 상속받는 부모 클래스는 AttackUnit 클래스와 Flyable 클래스
    - 이 중에서 AttackUnit 클래스는 Unit 클래스를 상속받음
      - FlyableAttackUnit 클래스에서도 Unit 클래스의 모든 내용을 그대로 사용 가능
- 공중 공격 유닛의 이동
  - 메서드 동작에 안내 문구를 추가
  - 공중으로 날아다니므로 또 다른 부모 클래스인 Flyable 클래스에 정의한 fly() 메서드를 호출
  - 유닛 이름과 이동할 위치 정보를 함께 전달

<br>

> 적용 코드
```
  # 공중 공격 유닛
  class FlyableAttackUnit(AttackUnit, Flyable):
      def __init__(self, name, hp, damage, flying_speed):
          AttackUnit.__init__(self, name, hp, damage, 0)
          Flyable.__init__(self, flying_speed)
   
  
      def move(self, location): # Unit 클래스의 move() 메서드를 오버라이딩
          print("[공중 유닛 이동]")
          self.fly(self.name, location)
```

<br>

> move()로 유닛들 이동(이름까지 전달해야 하는 번거로움 X)
```
  hoverbike.move("11시")
  # spacecruiser.fly(spacecruiser.name, "9시")
  spacecruiser.move("9시") # 오버라이딩한 move() 메서드 호출
```

<br>

> 실행결과
```
  [지상 유닛 이동]
  호버 바이크 : 11시 방향으로 이동합니다. [속도 10]
  [공중 유닛 이동]
  우주 순양함 : 9시 방향으로 날아갑니다. [속도 3]
```

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  # 일반 유닛
  class Unit:
      def __init__(self, name, hp, speed): # speed 추가
          self.name = name
          self.hp = hp
          self.speed = speed # 지상 이동 속도
  
      def move(self, location): # 이동 동작 정의
          print("[지상 유닛 이동]")
          print("{0} : {1} 방향으로 이동합니다. [속도 {2}]" \
              .format(self.name, location, self.speed))
  
  # 공격 유닛
  class AttackUnit(Unit): # Unit 클래스 상속
      def __init__(self, name, hp, damage, speed): # speed 추가
          Unit.__init__(self, name, hp, speed) # speed 추가
          self.damage = damage
  
      def attack(self, location):
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage))
  
      def damaged(self, damage):
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0:
              print("{0} : 파괴됐습니다.".format(self.name))
  
  # 비행 기능
  class Flyable:
      def __init__(self, flying_speed): # 비행 속도
          self.flying_speed = flying_speed
  
      def fly(self, name, location):
          print("{0} : {1} 방향으로 날아갑니다. [속도 {2}]" \
              .format(name, location, self.flying_speed))
  
  # 공중 공격 유닛
  class FlyableAttackUnit(AttackUnit, Flyable):
      def __init__(self, name, hp, damage, flying_speed):
          AttackUnit.__init__(self, name, hp, damage, 0)
          Flyable.__init__(self, flying_speed)
  
      def move(self, location): # Unit 클래스의 move() 메서드를 오버라이딩
          print("[공중 유닛 이동]")
          self.fly(self.name, location)
  
  # 호버 바이크: 지상 유닛, 기동성 좋음
  hoverbike = AttackUnit("호버 바이크", 80, 20, 10) # 지상 이동 속도 10
  
  # 우주 순양함: 공중 유닛, 체력도 굉장히 좋음, 공격력도 좋음
  spacecruiser = FlyableAttackUnit("우주 순양함", 500, 25, 3) # 비행 속도 3
  
  hoverbike.move("11시")
  spacecruiser.move("9시") # 오버라이딩한 move() 메서드 호출
```

</details>

<br>

#### 💡 메서드 오버라이딩
|-|
|-|
|![image](https://github.com/user-attachments/assets/5e0776b2-ed20-412e-8e4b-9a157d03c061)|
|- 상속 관계는 변함 X<br>- Unit 클래스에 move() 메서드를 정의함으로써 Unit 클래스로 생성한 객체들은 모두 move() 메서드를 사용해 지상에서 이동 가능<br>- 공중 공격 유닛인 FlyableAttackUnit 클래스로 생성한 객체들은 지상 이동이 아닌 공중에서 비행<br>- Flyable 클래스의 fly() 메서드를 사용<br>- 유닛이 많아지면 개별적으로 관리하기가 어려우므로 move() 메서드를 오버라이딩해서 재정의한 메서드에서 fly()를 호출하도록 변경<br>- 같은 move() 메서드를 호출하더라도 AttackUnit 클래스로 만들어진 유닛은 부모 클래스인 Unit 클래스의 move() 메서드 호출<br>- FlyableAttackUnit 클래스로 만들어진 유닛은 오버라이딩한 FlyableAttackUnit 클래스의 move() 메서드를 호출|

<br>

#### ✏️ 1. 다음 Burger 클래스를 상속해 CheeseBurger를 만들기 위한 방법으로 옳은 것은?
```
  class Burger:
      def __init__(self):
          self.add("패티")
          self.add("양상추")
  
      def add(self, item):
          print(f"{item} 추가")
```
```
  ① class CheeseBurger(Burger):
  
  ② class CheeseBurger[Burger]:
  
  ③ class CheeseBurger in Burger:
  
  ④ class CheeseBurger extends Burger:
```

<details>
  <summary>정답</summary>

<br>

> ① class CheeseBurger(Burger):

</details>

<br>

#### ✏️ 2. 다음 중 상속에 대한 설명으로 잘못된 것은?
```
  ① 다중 상속은 여러 클래스로부터 상속받는 것을 말한다.
  
  ② 클래스를 여러 개 상속받을 때는 콜론(:)으로 구분해 적는다.
  
  ③ 코드의 중복 입력 없이 부모 클래스의 기능을 그대로 이용할 수 있다.
  
  ④ 지식 클래스에서 부모 클래스의 메서드에 접근할 수 있다.
```

<details>
  <summary>정답</summary>

<br>

> ② 클래스를 여러 개 상속받을 때는 콜론(:)으로 구분해 적는다.
```
  다중 상속으로 여러 클래스를 상속받을 때는 쉼표(,)로 구분해 표시
```

</details>

<br>

#### ✏️ 3. 보기에서 설명하는 용어로 알맞은 것은?
|보기|
|-|
|부모 클래스의 메서드를 자식 클래스에서 새롭게 정의해 기존 동작을 개선하거나 새로운 동작을 수행하도록 하는 것|

```  
  ① 메서드 오버로딩(overloading)
  
  ② 메서드 오버라이딩(overriding)
  
  ③ 메서드 오버라이팅(overwriting)
  
  ④ 메서드 리라이팅(rewriting)
```

<details>
  <summary>정답</summary>

<br>

> ② 메서드 오버라이딩(overriding)

</details>

<br>
