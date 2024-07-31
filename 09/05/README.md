# 부모 클래스 호출하기: super( )
- 클래스에서 이름을 직접 적지 않고도 부모 클래스에 접근하는 방법
  - 상속하는 부모 클래스의 메서드를 사용할 때 필요
  - super()를 사용하는 문장에서는 self를 함께 사용 X

<br>

#### 💡 일상생활에서 생각해보자
```
  우리가 누군가의 부모님을 칭할 때 성함을 직접 부르는 경우는 많지 않음
  
  예를 들어,
  주말에 친구들과 놀러가기로 했을 때 “우리 놀러 가는 거 부모님께 허락받았어?”라고 물어보지
  “OOO님께 허락받았어?”라고 하지는 않음
```

<br>

### 예시
#### 건물 유닛 클래스를 만들 때 pass로만 남겨 둔 __init__() 생성자의 코드 완성
- Unit 클래스를 상속받으므로 Unit 클래스의 __init__() 생성자를 활용
- 건물은 이동할 수 없으므로 speed 정보는 0으로 하고 다음 줄에서 location 인스턴스 변수를 정의

<br>

> 적용 코드
```
  class BuildingUnit(Unit):
      def __init__(self, name, hp, location):
          Unit.__init__(self, name, hp, 0) # 지상 이동 속도 0, 건물은 지상 이동 불가
          self.location = location
```

<br>

> 수정 코드
```
  class BuildingUnit(Unit):
      def __init__(self, name, hp, location):
          # Unit.__init__(self, name, hp, 0) # 지상 이동 속도 0, 건물은 지상 이동 불가
          super().__init__(name, hp, 0) # 부모 클래스 접근, self 없이 사용
          self.location = location
```

<br>

### 부모 클래스를 2개 이상 상속하는 다중 상속일 때
- 다중 상속을 받은 클래스에서 super()로 부모 클래스에 접근할 때는 순서상 가장 먼저 상속받은 클래스에 접근
- 모든 부모 클래스의 생성자를 호출하려면 super()를 사용하지 않고 각 부모 클래스의 이름을 명시해서 접근

<br>

#### 테스트1
> super.py(새로운 파이썬 파일)
```
  class Unit:
      def __init__(self):
          print("Unit 생성자")
  
  class Flyable:
      def __init__(self):
          print("Flyable 생성자")
  
  class FlyableUnit(Unit, Flyable):
      def __init__(self):
          super().__init__()
  
  # 수송선
  troopship = FlyableUnit()
```
- 일반 유닛인 Unit 클래스와 비행 기능인 Flyable 클래스를 정의
  - 이 둘을 부모 클래스로 하는 공중 유닛인 FlyableUnit을 정의하고 생성자에서 super()로 부모 클래스의 생성자를 호출
- 공중 유닛 중에서 유닛의 수송을 담당하는 수송선을 생성하는 코드를 적고 실행

<br>

> 실행결과
```
  Unit 생성자
```
- 부모 클래스는 Unit과 Flyable인데, super()로 생성자를 호출했을 때 Unit 클래스의 생성자가 호출

---

#### 테스트2
- 부모 클래스의 상속 순서를 Unit, Flyable에서 Flyable, Unit으로 바꾼 후 다시 실행
> super.py
```
  # class FlyableUnit(Unit, Flyable):
  class FlyableUnit(Flyable, Unit): # 상속 순서 변경
      def __init__(self):
          super().__init__()
```

<br>

> 실행결과
```
  Flyable 생성자
```
- Flyable 클래스의 생성자가 호출

---

#### 테스트3
- 모든 부모 클래스의 생성자를 호출
> super.py
```
  # class FlyableUnit(Unit, Flyable):
  class FlyableUnit(Flyable, Unit):
      def __init__(self):
          # super().__init__()
          Unit.__init__(self) # Unit 클래스 생성자 호출
          Flyable.__init__(self) # Flyable 클래스 생성자 호출
```

<br>

> 실행결과
```
  Unit 생성자
  Flyable 생성자
```

<br>

<details>
  <summary>전체 코드</summary>

<br>

```
  class Unit:
      def __init__(self):
          print("Unit 생성자")
  
  class Flyable:
      def __init__(self):
          print("Flyable 생성자")
  
  class FlyableUnit(Flyable, Unit): # 상속 순서 변경
      def __init__(self):
          Unit.__init__(self) # Unit 클래스 생성자 호출
          Flyable.__init__(self) # Flyable 클래스 생성자 호출
  
  # 수송선
  troopship = FlyableUnit()
```

</details>

<br>

#### ✏️ 1. 자식 클래스에서 부모 클래스의 메서드를 호출하기 위해 [가]에 들어갈 값으로 알맞은 것은?
```
  class Noodle:
      def cook(self):
          print("끓는 물에 라면을 넣어요.")
  
  class EggNoodle(Noodle):
      def cook(self):
          [가].cook()
          print("계란을 넣어요.")
```
```
  ① base
  
  ② parent
  
  ③ super
  
  ④ super()
```

<details>
  <summary>정답</summary>

<br>

> ④ super()

</details>

<br>
