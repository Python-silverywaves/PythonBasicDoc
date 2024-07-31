# 동작 없이 일단 넘어가기: pass
- __init__() 생성자의 세부 내용은 일단 유지 → 다른 작업을 먼저 하고 나서 나중에 코드를 작성
  - pass : 아무것도 하지 않고 일단 그냥 넘어간다

<br>

> 유닛 생성 조건
```
  게임에서 유닛은 무한정 생성 불가
  처음 게임을 시작할 때는 인구 8에 해당하는 유닛을 만들 수 있고 8을 초과하면 더 이상 유닛을 뽑지 못함
  더 많은 유닛을 계속 뽑으려면 인구 제한을 늘려야 함
  인구 제한을 늘리려면 보급고라는 건물 유닛을 지어야 함
  보급고가 하나씩 늘어날 때마다 인구 8만큼 유닛을 더 만들 수 있음
```

<br>

### 예시
#### 건물 유닛을 짓기 위한 클래스 생성
- 일반 유닛처럼 이름과 체력이 있어서 적군으로부터 공격받아 체력이 0이 되면 파괴
- Unit 클래스에 공통 속성이 있으니 다른 유닛과 마찬가지로 상속받기
- 건물 유닛을 지을 위치 location

<br>

> 적용 코드
```
  # 건물 유닛
  class BuildingUnit(Unit):
      def __init__(self, name, hp, location):
          pass
  
  # 보급고: 건물 유닛, 1개 건물 유닛 = 8유닛
  supply_depot = BuildingUnit("보급고", 500, "7시") # 체력 500, 생성 위치 7시
```
- supply_depot 객체가 오류 없이 잘 생성
  -  pass 때문에 __init__() 생성자는 실제로 완성되지 않았지만, 마치 완성된 것처럼 보임

<br>

#### 게임 시작 및 종료 함수 추가
- game_start()에서는 실행할 문장 부분에 print() 문으로 안내 문구를 출력
  - 정의한 동작을 수행
- game_over()에서는 pass만 작성
  - 아무 동작 없이 그냥 넘어감
    - 함수뿐 아니라 if 문, for 문, while 문 등에서도 pass로 당장은 세부 동작을 정의하지 않은 채로 뒀다가 나중에 다시 코드 완성 가능

<br>

> 적용 코드
```
  def game_start():
      print("[알림] 새로운 게임을 시작합니다.")
  
  def game_over():
      pass
  
  game_start()
  game_over()
```

<br>

> 실행결과
```
  [알림] 새로운 게임을 시작합니다.
```

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  # 건물 유닛
  class BuildingUnit(Unit):
      def __init__(self, name, hp, location):
          pass
  
  # 보급고: 건물 유닛, 1개 건물 유닛 = 8유닛
  supply_depot = BuildingUnit("보급고", 500, "7시") # 체력 500, 생성 위치 7시
  
  def game_start():
      print("[알림] 새로운 게임을 시작합니다.")
  
  def game_over():
      pass
  
  game_start()
  game_over()
```

</details>

<br>

#### ✏️ 1. 다음 중 pass의 사용 예로 올바르지 않은 것은?
```
  ①
    while True:
        pass
  
  ②
    def add():
        pass
  
  ③
    if pass:
        print("to be defined")
  
  ④
    class Book:
        pass
```

<details>
  <summary>정답</summary>

<br>

>   ③
```
    if pass:
        print("to be defined")
```

</details>

<br>
