# 게임완성
### 게임 준비하기
#### Unit 클래스
- 실제 게임에서는 유닛이 생성될 때마다 각 유닛의 고유한 소리를 울려서 유닛 생성 알림
  - 여기서는 소리 대신 __init__() 생성자에 print() 문을 추가해 어떤 유닛을 생성했는지 안내 문구 출력
- move() 메서드에서는 유닛 이동과 관련한 안내 문구를 2번이나 출력하므로 첫 번째 출력문인 [지상 유닛 이동] 문구는 삭제
- 공격 유닛인 AttackUnit 클래스를 만들면서 적군으로부터 공격받을 때 호출되는 damaged() 메서드 정의
  - 일반 유닛은 공격할 수는 없지만, 공격받을 수는 있음
    - damaged() 메서드를 Unit 클래스로 이동하고 AttackUnit 클래스에서는 제외

<br>

> 적용 코드
```
  # 일반 유닛
  class Unit:
      def __init__(self, name, hp, speed):
          self.name = name
          self.hp = hp
          self.speed = speed
          print("{0} 유닛을 생성했습니다.".format(name)) ---- ➊ 안내 문구 출력
   
  
      def move(self, location):
          # print("[지상 유닛 이동]") ----------------------- ➋ 출력문 삭제
          print("{0} : {1} 방향으로 이동합니다. [속도 {2}]" \
              .format(self.name, location, self.speed))
   
  
      def damaged(self, damage): --------------- ➌ AttackUnit 클래스에서 Unit 클래스로 이동
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0:
              print("{0} : 파괴됐습니다.".format(self.name))
```

<br>

#### AttackUnit 클래스
- Unit 클래스로 damaged() 메서드를 이동
- 기존에는 AttackUnit 클래스로 보병, 탱크 등 지상 유닛을 생성했지만, 이제는 각 유닛을 직접 클래스로 정의
  
<br>

> 적용 코드
```
  # 공격 유닛
  class AttackUnit(Unit):
      def __init__(self, name, hp, damage, speed):
          Unit.__init__(self, name, hp, speed)
          self.damage = damage
  
      def attack(self, location):
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage))
      """
      def damaged(self, damage): ------------------- Unit 클래스로 이동
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0:
              print("{0} : 파괴됐습니다.".format(self.name))
      """
```

<br>

#### Soldier 클래스
- 보병은 공격 유닛
  - AttackUnit 클래스를 상속받아 AttackUnit 클래스의 생성자로 체력, 공격력, 이동 속도를 설정
- 강화제
  - 특수 기술을 사용하면 일정 시간 동안 이동 속도와 공격 속도가 아주 빠르게 증가
  - 대신 체력이 10만큼 소모되므로 현재 남은 체력이 10보다 클 때만 사용할 수 있음
    - booster()라는 메서드 생성
      - 체력이 10보다 크면 체력 10을 소모한 후 강화제를 사용한다는 안내 문구를 출력
      - 체력이 10보다 작으면 강화제 사용이 불가능하다는 문구를 출력

<br>

> 적용 코드
```
  # 보병 유닛
  class Soldier(AttackUnit): --------- ➊ AttackUnit 클래스 상속
      def __init__(self):
          AttackUnit.__init__(self, "보병", 40, 5, 1) # 이름, 체력, 공격력, 이동 속도
  
      # 강화제: 일정 시간 동안 이동 속도와 공격 속도 증가, 체력 10 감소
      def booster(self): ------------- ➋ 강화제 기능 메서드로 정의
          if self.hp > 10:
              self.hp -= 10 # 체력 10 소모
              print("{0} : 강화제를 사용합니다. (HP 10 감소)".format(self.name))
          else:
              print("{0} : 체력이 부족해 기술을 사용할 수 없습니다".format(self.name))
```

<br>

#### Tank 클래스
- 시지 모드
  - 탱크를 지상에 고정하고 2배에 달하는 공격력과 더 넓은 사정거리로 공격
    - 업그레이드로 시지 모드를 개발해야만 사용 가능

- 탱크는 공격 유닛
  - AttackUnit 클래스를 상속
  - 시지 모드를 개발하면 해당 시점부터 모든 탱크를 시지 모드로 전환 가능
    - 이미 만든 탱크도, 앞으로 만들 탱크도 모두 포함
    - 한 클래스로 만들어진 객체에 일괄적으로 무언가를 적용하려면 인스턴스 변수가 아닌 클래스 변수로 정의
      - siege_developed라는 이름으로 클래스 변수를 정의 : 정의 위치가 어디인지 꼭 확인
        - set_siege_mode() 메서드가 호출되면 현재 시지 모드가 개발됐는지를 먼저 확인
          - 시지 모드가 개발되지 않았으면 호출한 곳으로 바로 되돌아감
        - 시지 모드가 개발된 상태라면 탱크 객체의 시지 모드 설정 여부를 확인
        - 현재 일반 모드이면 시지 모드로 전환하고 공격력을 증가시키는 문구를 출력
        - 시지 모드이면 일반 모드로 전환하고 공격력을 감소시키고 필요한 문구를 출력
        - 인스턴스 변수인 siege_mode의 값을 True 또는 False로 변경해 시지 모드 설정 또는 해제 상태를 저장

- 시지 모드 개발이 완료됐다고 해서 모든 탱크가 항상 시지 모드여야 하는 것은 X
  - 시지 모드인지 아닌지를 확인하기 위해 siege_mode라는 인스턴스 변수를 정의
    - 처음에는 일반 모드일 테니 시지 모드 해제 상태(False)

<br>

> 적용 코드
```
  # 탱크 유닛
  class Tank(AttackUnit): ------------ ➊ AttackUnit 클래스 상속
      # 시지 모드: 탱크를 지상에 고정, 이동 불가, 공격력 증가
      siege_developed = False -------- ➋ 시지 모드 개발 여부, 클래스 변수로 정의
  
      def __init__(self):
          AttackUnit.__init__(self, "탱크", 150, 35, 1) # 이름, 체력, 공격력, 이동 속도
          self.siege_mode = False ---- ➌ 시지 모드(해제 상태), 인스턴스 변수로 정의

     # 시지 모드 설정
      def set_siege_mode(self):
          if Tank.siege_developed == False: ---- ➊ 시지 모드가 개발되지 않았으면 바로 반환
              return
          # 현재 일반 모드일 때
          if self.siege_mode == False: --------- ➋ 시지 모드 여부 확인
              print("{0} : 시지 모드로 전환합니다.".format(self.name)) ---- ➌ 시지 모드 전환
              self.damage *= 2 ----------------- ➌ 공격력 2배 증가
              self.siege_mode = True ----------- ➎ 시지 모드 설정
          # 현재 시지 모드일 때
          else:
              print("{0} : 시지 모드를 해제합니다.".format(self.name)) ---- ➍ 일반 모드 전환
              self.damage //= 2 ---------------- ➍ 공격력 절반으로 감소
              self.siege_mode = False ---------- ➎ 시지 모드 해제
```

<br>

<details>
  <summary>클래스 변수</summary>

<br>

```
  클래스 변수는 클래스명과 함께 어디서든 사용 가능
  Tank.siege_developed라고 하면 Tank 클래스의 클래스 변수에 직접 접근해 시지 모드가 개발됐는지를 확인 가능
```

<br>

> 클래스 변수 vs 인스턴스 변수
```
  인스턴스 변수
    - 객체마다 각각 다른 값을 가질 수 있음
    - 클래스의 메서드에 정의하거나 객체를 통해 직접 정의
  
  클래스 변수
    - 모든 객체가 동일한 값을 가짐(클래스로부터 만들어진 모든 객체에 값이 일괄 적용)
    - 클래스명 바로 밑에 정의
```

</details>

<br>

#### Flyable 클래스
- 수정 사항 X

<br>

> 적용 코드
```
  # 비행 기능
  class Flyable:
      def __init__(self, flying_speed):
          self.flying_speed = flying_speed
  
      def fly(self, name, location):
          print("{0} : {1} 방향으로 날아갑니다. [속도 {2}]" 
              .format(name, location, self.flying_speed))
```

<br>

#### FlyableAttackUnit 클래스
- move() 메서드에서 [공중 유닛 이동] 문구 삭제
  - move() 메서드를 호출하면 실제로는 부모 클래스인 Flyable 클래스의 fly() 메서드가 실행되면서 어느 방향으로 날아가는지 출력

<br>

> 적용 코드
```
  # 공중 공격 유닛
  class FlyableAttackUnit(AttackUnit, Flyable):
      def __init__(self, name, hp, damage, flying_speed):
          AttackUnit.__init__(self, name, hp, damage, 0)
          Flyable.__init__(self, flying_speed)
  
      def move(self, location):
          # print("[공중 유닛 이동]") -------- 출력문 삭제
          self.fly(self.name, location)
```

<br>

#### Stealth 클래스
- 전투기는 공중 공격 유닛
  - FlyableAttackUnit 클래스를 상속
- 은폐
  - 편의상 업그레이드가 완료됐다고 가정
  - 부모 클래스인 FlyableAttackUnit 클래스의 생성자로 기본 정보를 설정
- 은폐 여부를 확인하기 위해 cloaked 인스턴스 변수를 추가로 정의
- 은폐 모드를 설정하기 위한 cloaking() 메서드를 정의
  - 은폐 모드 여부에 따라서 설정(True)과 해제(False)를 하도록 if-else 문으로 작성
- 은폐 모드 설정 여부를 True 또는 False로 cloaked 인스턴스 변수에 저장
  - 확인을 위한 문구도 함께 출력

<br>

> 적용 코드
```
  # 전투기 유닛
  class Stealth(FlyableAttackUnit):---- ➊ FlyableAttackUnit 클래스 상속
      def __init__(self):
          FlyableAttackUnit.__init__(self, "전투기", 80, 20, 5) ---- ➋ 부모 클래스 생성자로 기본 정보 설정
          self.cloaked = False--------- ➌ 은폐 모드(해제 상태), 인스턴스 변수 정의
  
      def cloaking(self):-------------- ➍ 은폐 모드를 메서드로 정의
          # 현재 은폐 모드일 때
          if self.cloaked == True:
              print("{0} : 은폐 모드를 해제합니다.".format(self.name))
              self.cloaked = False----- ➎ 은폐 모드 해제
          # 현재 은폐 모드가 아닐 때
          else:
              print("{0} : 은폐 모드를 설정합니다.".format(self.name))
              self.cloaked = True------ ➎ 은폐 모드 설정
```

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  # 일반 유닛
  class Unit:
      def __init__(self, name, hp, speed):
          self.name = name
          self.hp = hp
          self.speed = speed
          print("{0} 유닛을 생성했습니다.".format(name))
  
      def move(self, location):
          print("{0} : {1} 방향으로 이동합니다. [속도 {2}]" \
              .format(self.name, location, self.speed))
  
      def damaged(self, damage):
          print("{0} : {1}만큼 피해를 입었습니다.".format(self.name, damage))
          self.hp -= damage
          print("{0} : 현재 체력은 {1}입니다.".format(self.name, self.hp))
          if self.hp <= 0:
              print("{0} : 파괴됐습니다.".format(self.name))
  
  # 공격 유닛
  class AttackUnit(Unit):
      def __init__(self, name, hp, damage, speed):
          Unit.__init__(self, name, hp, speed)
          self.damage = damage
  
      def attack(self, location):
          print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]" \
              .format(self.name, location, self.damage))
  
  # 보병 유닛
  class Soldier(AttackUnit):
      def __init__(self):
          AttackUnit.__init__(self, "보병", 40, 5, 1) # 이름, 체력, 공격력, 이동 속도
  
      # 강화제: 일정 시간 동안 이동 속도와 공격 속도 증가, 체력 10 감소
      def booster(self):
          if self.hp > 10:
              self.hp -= 10 # 체력 10 소모
              print("{0} : 강화제를 사용합니다. (HP 10 감소)".format(self.name))
          else:
              print("{0} : 체력이 부족해 기술을 사용할 수 없습니다".format(self.name))
  
  # 탱크 유닛
  class Tank(AttackUnit):
      # 시지 모드: 탱크를 지상에 고정, 이동 불가, 공격력 증가
      siege_developed = False # 시지 모드 개발 여부
  
      def __init__(self):
          AttackUnit.__init__(self, "탱크", 150, 35, 1) # 이름, 체력, 공격력, 이동 속도
          self.siege_mode = False # 시지 모드(해제 상태)
  
      # 시지 모드 설정
      def set_siege_mode(self):
          if Tank.siege_developed == False: # 시지 모드가 개발되지 않았으면 바로 반환
              return
          if self.siege_mode == False:
              print("{0} : 시지 모드로 전환합니다.".format(self.name))
              self.damage *= 2 # 공격력 2배 증가
              self.siege_mode = True # 시지 모드 설정
          else:
              print("{0} : 시지 모드를 해제합니다.".format(self.name))
              self.damage //= 2 # 공격력 절반으로 감소
              self.siege_mode = False # 시지 모드 해제
  
  # 비행 기능
  class Flyable:
      def __init__(self, flying_speed):
          self.flying_speed = flying_speed
  
      def fly(self, name, location):
          print("{0} : {1} 방향으로 날아갑니다. [속도 {2}]" \
              .format(name, location, self.flying_speed))
  
  # 공중 공격 유닛
  class FlyableAttackUnit(AttackUnit, Flyable):
      def __init__(self, name, hp, damage, flying_speed):
          AttackUnit.__init__(self, name, hp, damage, 0)
          Flyable.__init__(self, flying_speed)
  
      def move(self, location):
          self.fly(self.name, location)
  
  # 전투기 유닛
  class Stealth(FlyableAttackUnit): # FlyableAttackUnit 클래스 상속
      def __init__(self):
          # 부모 클래스 생성자로 기본 정보 설정
          FlyableAttackUnit.__init__(self, "전투기", 80, 20, 5)
          self.cloaked = False # 은폐 모드(해제 상태), 인스턴스 변수 정의
  
      def cloaking(self): # 은폐 모드를 메서드로 정의
          if self.cloaked == True:
              print("{0} : 은폐 모드를 해제합니다.".format(self.name))
              self.cloaked = False
          else:
              print("{0} : 은폐 모드를 설정합니다.".format(self.name))
              self.cloaked = True
```

</details>

<br>

### 게임 실행하기

- 클래스들을 사용해 게임 실행

- 게임 시작부터 종료까지 수행할 동작을 순차적으로 정리

```
  • 게임 시작
  
  • 유닛 생성(보병 3기, 탱크 2기, 전투기 1기)
  
  • 전군 1시 방향으로 이동
  
  • 탱크 시지 모드 개발
  
  • 공격 준비(보병 강화제, 탱크 시지 모드, 전투기 은폐 모드)
  
  • 전군 1시 방향 공격
  
  • 전군 피해
  
  • 게임 종료
```

<br>

#### 게임 시작과 유닛 생성
> 게임의 시작과 종료를 알리는 함수를 각각 정의
```
  # 게임 시작
  def game_start():
      print("[알림] 새로운 게임을 시작합니다.")
  
  # 게임 종료
  def game_over():
      print("Player : Good Game")
      print("[Player] 님이 게임에서 퇴장했습니다.")
```

<br>

> 게임을 시작함과 동시에 보병 3기, 탱크 2기, 전투기 1기 생성
```
  # 게임 시작
  game_start()
  
  # 보병 3기 생성
  so1 = Soldier()
  so2 = Soldier()
  so3 = Soldier()
  
  # 탱크 2기 생성
  ta1 = Tank()
  ta2 = Tank()
  
  # 전투기 1기 생성
  st1 = Stealth()
```

<br>

> 실행 결과
```
  [알림] 새로운 게임을 시작합니다.
  보병 유닛을 생성했습니다.
  보병 유닛을 생성했습니다.
  보병 유닛을 생성했습니다.
  탱크 유닛을 생성했습니다.
  탱크 유닛을 생성했습니다.
  전투기 유닛을 생성했습니다.
```

<br>

- 유닛이 이동하거나 공격할 때 한꺼번에 처리하도록 리스트로 관리
> attack_units라는 이름으로 리스트를 만들고 모든 유닛을 추가
```
  # 유닛 일괄 관리(생성된 모든 유닛 추가)
  attack_units = []
  attack_units.append(so1)
  attack_units.append(so2)
  attack_units.append(so3)
  attack_units.append(ta1)
  attack_units.append(ta2)
  attack_units.append(st1)
```

<br>

#### 전군 이동과 탱크 시지 모드 개발
- 모든 유닛은 Unit 클래스를 상속받고 리스트로 관리
  - Unit 클래스의 move() 메서드를 사용 가능
  - 반복문 사용

<br>

> 1시 방향으로 모든 유닛을 이동
```
  # 전군 이동
  for unit in attack_units:
      unit.move("1시")
```

<br>

> 실행결과
```
  보병 : 1시 방향으로 이동합니다. [속도 1]
  보병 : 1시 방향으로 이동합니다. [속도 1]
  보병 : 1시 방향으로 이동합니다. [속도 1]
  탱크 : 1시 방향으로 이동합니다. [속도 1]
  탱크 : 1시 방향으로 이동합니다. [속도 1]
  전투기 : 1시 방향으로 날아갑니다. [속도 5]
```

<br>

- 이동하는 와중에 탱크의 시지 모드 개발 완료
  - Tank 클래스에 정의한 클래스 변수 siege_developed에는 Tank.siege_developed로 접근 가능, 값 = True

<br>

> 시지 모드
```
  # 탱크 시지 모드 개발
  Tank.siege_developed = True
  print("[알림] 탱크의 시지 모드 개발이 완료됐습니다.")
```

<br>

> 실행결과
```
  [알림] 탱크의 시지 모드 개발이 완료됐습니다.
```

<br>

#### 공격 준비와 전군 공격
- 리스트로 관리되는 유닛들이 서로 다른 기술을 사용
  - 구분하려면 isinstance() 함수를 사용
    - 객체가 특정 클래스의 인스턴스인지를 확인
    - 각 유닛 객체가 Soldier 클래스의 인스턴스인지, Tank 또는 Stealth 클래스의 인스턴스인지를 확인해 각 유닛에 맞는 특수 기술을 사용

<br>

> 형식
```
  isinstance(객체명, 클래스명)
```

<br>

> 유닛 구분
```
  # 공격 모드 준비(보병: 강화제, 탱크: 시지 모드, 전투기: 은폐 모드)
  for unit in attack_units:
      if isinstance(unit, Soldier): # Soldier 클래스의 인스턴스이면 강화제
          unit.booster()
      elif isinstance(unit, Tank): # Tank 클래스의 인스턴스이면 시지 모드
          unit.set_siege_mode()
      elif isinstance(unit, Stealth): # Stealth 클래스의 인스턴스이면 은폐 모드
          unit.cloaking()
```

<br>

> 부모 클래스인 AttackUnit의 attack() 메서드를 활용하여 공격 지시
```
  # 전군 공격
  for unit in attack_units:
      unit.attack("1시")
```

<br>

> 실행결과
```
  보병 : 강화제를 사용합니다. (HP 10 감소)
  보병 : 강화제를 사용합니다. (HP 10 감소)
  보병 : 강화제를 사용합니다. (HP 10 감소)
  탱크 : 시지 모드로 전환합니다.
  탱크 : 시지 모드로 전환합니다.
  전투기 : 은폐 모드를 설정합니다.
  보병 : 1시 방향 적군을 공격합니다. [공격력 5]
  보병 : 1시 방향 적군을 공격합니다. [공격력 5]
  보병 : 1시 방향 적군을 공격합니다. [공격력 5]
  탱크 : 1시 방향 적군을 공격합니다. [공격력 70]
  탱크 : 1시 방향 적군을 공격합니다. [공격력 70]
  전투기 : 1시 방향 적군을 공격합니다. [공격력 20]
```

<br>

#### 전군 피해와 게임 종료
- 공격하는 과정에서 우리 편도 피해 받음
  - Unit 클래스의 damaged() 메서드를 호출, 피해는 5에서 20 사이의 난수로 값을 지정
    - random 모듈을 사용하기 위해 소스 코드 첫 줄에 import

<br>

> 피해량
```
  from random import *
  (중략)
  
  # 전군 공격
  for unit in attack_units:
      unit.attack("1시")
  
  # 전군 피해
  for unit in attack_units:
      unit.damaged(randint(5, 20)) # 피해는 무작위로 받음(5~20)
```

<br>

> 실행결과
```
  보병 : 16만큼 피해를 입었습니다.
  보병 : 현재 체력은 14입니다.
  보병 : 15만큼 피해를 입었습니다.
  보병 : 현재 체력은 15입니다.
  보병 : 11만큼 피해를 입었습니다.
  보병 : 현재 체력은 19입니다.
  탱크 : 15만큼 피해를 입었습니다.
  탱크 : 현재 체력은 135입니다.
  탱크 : 17만큼 피해를 입었습니다.
  탱크 : 현재 체력은 133입니다.
  전투기 : 19만큼 피해를 입었습니다.
  전투기 : 현재 체력은 61입니다.
```

<br>

- 우리 유닛들이 모두 전사했다고 가정
  - 패배를 인정하고 ‘Good Game’을 출력한 후 게임 종료

<br>

> 종료
```
  # 게임 종료
  game_over()
```

<br>

> 실행결과
```
  Player : Good Game
  [Player] 님이 게임에서 퇴장했습니다.
```

<br>
