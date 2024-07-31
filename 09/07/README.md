# 게임 최종 리뷰
|게임 전체 클래스의 상속 관계|
|-|
|![image](https://github.com/user-attachments/assets/25aac02b-156c-4295-8b71-2aeff85bd55e)|
|- 가장 기본이 되는 일반 유닛인 Unit 클래스를 공격 유닛인 AttackUnit 클래스가 상속받음<br>- AttackUnit 클래스를 상속받아 지상 공격 유닛인 보병과 탱크를 위한 Soldier, Tank 클래스를 정의<br>- 공중 유닛을 위해 비행 기능을 제공하는 Flyable 클래스를 정의<br>- 공중 공격 유닛인 FlyableAttackUnit 클래스는 Flyable 클래스와 AttackUnit 클래스를 다중 상속받음<br>- FlyableAttackUnit 클래스를 상속받아 전투기 유닛을 위한 Stealth 클래스를 정의|
|- 최하위에 위치한 Soldier, Tank, Stealth 클래스는 각 유닛이 보유한 특수 기술을 메서드로 정의<br>- 공격, 이동, 피해 등 공통으로 처리되는 동작은 상속 관계에 따라 부모 클래스에 정의한 것을 그대로 사용<br>- 공중 공격 유닛은 공중으로 날아서 이동함<br>- Unit 클래스의 move() 메서드를 오버라이딩해 Flyable 클래스의 fly() 메서드를 호출하도록 재정의<br>- 재정의한 덕분에 모든 유닛은 지상과 공중 구분 없이 모두 move() 메서드로 이동 동작을 처리가능|

<br>

<details>
  <summary>전체 코드</summary>

<br>

> 전체 코드
```
  from random import *
  
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
          print("{0}  : 현재체력은 {1}입니다.".format(self.name, self.hp))
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
          # 현재 일반 모드일 때
          if self.siege_mode == False:
              print("{0} : 시지 모드로 전환합니다.".format(self.name))
              self.damage *= 2 # 공격력 2배 증가
              self.siege_mode = True # 시지 모드 설정
          # 현재 시지 모드일 때
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
  class Stealth(FlyableAttackUnit):
      def __init__(self):
          FlyableAttackUnit.__init__(self, "전투기", 80, 20, 5)
          self.cloaked = False # 은폐 모드(해제 상태)
  
      # 은폐 모드
      def cloaking(self):
          # 현재 은폐 모드일 때
          if self.cloaked == True:
              print("{0} : 은폐 모드를 해제합니다.".format(self.name))
              self.cloaked = False
          # 현재 은폐 모드가 아닐 때
          else:
              print("{0} : 은폐 모드를 설정합니다.".format(self.name))
              self.cloaked = True
  
  # 게임 시작
  def game_start():
      print("[알림] 새로운 게임을 시작합니다.")
  
  # 게임 종료
  def game_over():
      print("Player : Good Game")
      print("[Player] 님이 게임에서 퇴장했습니다.")
  
  # 실제 게임 진행
  game_start() # 게임 시작
  
  # 보병 3기 생성
  so1 = Soldier()
  so2 = Soldier()
  so3 = Soldier()
  
  # 탱크 2기 생성
  ta1 = Tank()
  ta2 = Tank()
  
  # 전투기 1기 생성
  st1 = Stealth()
      
  # 유닛 일괄 관리(생성된 모든 유닛 추가)
  attack_units = []
  attack_units.append(so1)
  attack_units.append(so2)
  attack_units.append(so3)
  attack_units.append(ta1)
  attack_units.append(ta2)
  attack_units.append(st1)
  
  # 전군 이동
  for unit in attack_units:
      unit.move("1시")
  
  # 탱크 시지 모드 개발
  Tank.siege_developed = True
  print("[알림] 탱크의 시지 모드 개발이 완료됐습니다.")
  
  # 공격 모드 준비(보병: 강화제, 탱크: 시지 모드, 전투기: 은폐 모드)
  for unit in attack_units:
      if isinstance(unit, Soldier): # Soldier 클래스의 인스턴스이면 강화제
          unit.booster()
      elif isinstance(unit, Tank): # Tank 클래스의 인스턴스이면 시지 모드
          unit.set_siege_mode()
      elif isinstance(unit, Stealth): # Stealth 클래스의 인스턴스이면 은폐 모드
          unit.cloaking()
  
  # 전군 공격
  for unit in attack_units:
      unit.attack("1시")
  
  # 전군 피해
  for unit in attack_units:
      unit.damaged(randint(5, 20)) # 피해는 무작위로 받음(5~20)
  
  # 게임 종료
  game_over()
```

<br>

> 유닛을 생성하고 전군 이동 명령으로 모든 유닛을 1시로 이동
> > 이동하는 중에 탱크의 시지 모드가 개발
```
  [알림] 새로운 게임을 시작합니다.
  보병 유닛을 생성했습니다.
  보병 유닛을 생성했습니다.
  보병 유닛을 생성했습니다.
  탱크 유닛을 생성했습니다.
  탱크 유닛을 생성했습니다.
  전투기 유닛을 생성했습니다.
  보병 : 1시 방향으로 이동합니다. [속도 1]
  보병 : 1시 방향으로 이동합니다. [속도 1]
  보병 : 1시 방향으로 이동합니다. [속도 1]
  탱크 : 1시 방향으로 이동합니다. [속도 1]
  탱크 : 1시 방향으로 이동합니다. [속도 1]
  전투기 : 1시 방향으로 날아갑니다. [속도 5]
  [알림] 탱크의 시지 모드 개발이 완료됐습니다.
```

<br>

> 적군 진영 바로 앞에서 공격 준비
> > 유닛별로 특수 기술을 사용하며 전쟁 준비 완료 후 전면전 개시
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

> 전쟁 과정에서 아군이 피해를 입음
> > 패배를 인정하고 게임에서 퇴장
```
  보병 : 17만큼 피해를 입었습니다.
  보병 : 현재 체력은 13입니다.
  보병 : 6만큼 피해를 입었습니다.
  보병 : 현재 체력은 24입니다.
  보병 : 15만큼 피해를 입었습니다.
  보병 : 현재 체력은 15입니다.
  탱크 : 9만큼 피해를 입었습니다.
  탱크 : 현재 체력은 141입니다.
  탱크 : 18만큼 피해를 입었습니다.
  탱크 : 현재 체력은 132입니다.
  전투기 : 12만큼 피해를 입었습니다.
  전투기 : 현재 체력은 68입니다.
  Player : Good Game
  [Player] 님이 게임에서 퇴장했습니다.
```

</details>

<br>
