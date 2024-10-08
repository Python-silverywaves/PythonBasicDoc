# 게임 소개
### 텍스트 게임 만들어보면서 개념 알아보기
- 게임 내용 : 세 종족 사이의 전쟁
  - 목표 : 유닛(unit)을 최대한 빠르게 많이 만들어 적을 궤멸시켜야 함
  - 세 종족 중 한 종족을 선택해 게임을 플레이하는 형태로 구현
    - 이 종족은 보병, 탱크, 전투기와 같은 유닛을 생산

<br>

### 보병 유닛 생성
- 보병 : 총을 쏘는 군인
  - 유닛의 이름과 체력, 공격력 정보를 각각의 변수에 저장하고 유닛이 생성됐다는 내용과 함께 유닛 정보를 출력

<br>

> 적용 코드 
```
  # 보병: 공격 유닛, 군인, 총을 쏠 수 있음
  name = "보병" # 이름
  hp = 40       # 체력
  damage = 5    # 공격력
  
  print("{} 유닛을 생성했습니다.".format(name))
  print("체력 {0}, 공격력 {1}\n".format(hp, damage))
```

<br>

> 실행결과 : 보병 유닛 생성 완료
```
  보병 유닛을 생성했습니다.  
  체력 40, 공격력 5
```

<br>

### 탱크 유닛 생성
- 탱크 : 이동하면서 공격하는 일반 모드 + 지상에 탱크를 고정하고 공격하는 시지(siege) 모드(사정거리 및 공격력 증가)
  - 이름과 체력, 공격력 정보를 변수에 담아 유닛 생성
    - name, hp, damage라는 변수가 이미 쓰였으므로 각각의 변수 앞에 tank_를 붙여서 탱크 유닛을 만들고 내용 출력

<br>

> 적용 코드
```
  # 보병: 공격 유닛, 군인, 총을 쏠 수 있음
  name = "보병" # 이름
  hp = 40       # 체력
  damage = 5    # 공격력
  
  print("{} 유닛을 생성했습니다.".format(name))
  print("체력 {0}, 공격력 {1}\n".format(hp, damage))
  
  # 탱크: 공격 유닛, 포를 쏠 수 있음, 두 가지 모드(일반/시지 모드)
  tank_name = "탱크"
  tank_hp = 150
  tank_damage = 35
   
  print("{} 유닛을 생성했습니다.".format(tank_name))
  print("체력 {0}, 공격력 {1}\n".format(tank_hp, tank_damage))
```

<br>

> 실행결과 : 탱크 유닛 생성 완료
```
  보병 유닛을 생성했습니다.
  체력 40, 공격력 5
  
  탱크 유닛을 생성했습니다.
  체력 150, 공격력 35
```

<br>

### 두 유닛을 사용해 공격 함수 정의
- 공격 부분은 두 유닛이 공통으로 사용

<br>

> 적용 코드
```
  # 공격 함수
  def attack(name, location, damage):
      print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]".format(name, location, damage))
```

<br>

> 보병과 탱크가 1시 방향을 공격하도록 attack() 함수 호출
```
  attack(name, "1시", damage) # 보병 공격 명령
  attack(tank_name, "1시", tank_damage) # 탱크 공격 명령
```

<br>

> 실행결과
```
  보병 : 1시 방향 적군을 공격합니다. [공격력 5]
  탱크 : 1시 방향 적군을 공격합니다. [공격력 35]
```

<br>

### 새로운 탱크 유닛 추가
> 적용 코드
```
  # 보병: 공격 유닛, 군인, 총을 쏠 수 있음
  name = "보병" # 이름
  hp = 40       # 체력
  damage = 5    # 공격력
  
  print("{} 유닛을 생성했습니다.".format(name))
  print("체력 {0}, 공격력 {1}\n".format(hp, damage))
  
  # 탱크: 공격 유닛, 포를 쏠 수 있음, 두 가지 모드(일반/시지 모드)
  tank_name = "탱크"
  tank_hp = 150
  tank_damage = 35
  
  print("{} 유닛을 생성했습니다.".format(tank_name))
  print("체력 {0}, 공격력 {1}\n".format(tank_hp, tank_damage))
  
  # 새로운 탱크2 추가
  tank2_name = "탱크"
  tank2_hp = 150
  tank2_damage = 35
  print("{} 유닛을 생성했습니다.".format(tank2_name))
  print("체력 {0}, 공격력 {1}\n".format(tank2_hp, tank2_damage))

  # 공격 함수
  def attack(name, location, damage):
      print("{0} : {1} 방향 적군을 공격합니다. [공격력 {2}]".format(name, location, damage))
  
  attack(name, "1시", damage) # 보병 공격 명령
  attack(tank_name, "1시", tank_damage) # 탱크 공격 명령
  attack(tank2_name, "1시", tank2_damage) # 탱크2 공격 명령
```

<br>

> 실행결과
```
  보병 유닛을 생성했습니다.
  체력 40, 공격력 5
  
  탱크 유닛을 생성했습니다.
  체력 150, 공격력 35
  
  탱크 유닛을 생성했습니다.
  체력 150, 공격력 35
  
  보병 : 1시 방향 적군을 공격합니다. [공격력 5]
  탱크 : 1시 방향 적군을 공격합니다. [공격력 35]
  탱크 : 1시 방향 적군을 공격합니다. [공격력 35]
```

<br>

#### 💡*실제 게임이라고 생각해보자*
- 유닛을 추가하면 추가할 때마다 같은 방법으로 코드를 추가하면 됨 ⇒ 중복코드 및 코드길이가 길어짐
- 왜? → 서로 다른 종류의 유닛들이 최소 수십 개에서 수백 개까지 존재하기 때문
  - 유닛마다 서로 다른 정보(이름, 체력, 공격력 등) 보유

<br>
