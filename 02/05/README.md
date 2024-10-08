# 주석(comment)
```
  코드가 어떤 내용을 포함하고 있는지,
  
  이 문장이 의미하는 것이 무엇인지,
  
  왜 이렇게 썼는지,
  
  주의할 점은 무엇인지,
  
  추가로 알아야 할 내용은 무엇인지 등을 설명해야 할 때 사용
```
- 프로그램 안에 작성하지만, 프로그램을 실행하는 데 아무런 영향 X

- 개발자에게는 코드의 의미를 전달하는 큰 역할

- 주석 처리하고 싶은 명령문이 있으면 문장 앞 또는 뒤에 #(샤프, sharp)

- 여러 줄을 한꺼번에 주석 처리하고 싶으면?

  - \# 을 여러 번 사용
 
  - 따옴표 3개(큰따옴표 또는 작은따옴표)를 사용하면 여러 줄을 한꺼번에 주석 처리

<br>

### 주석의 필요성
- 식탁에 쪽지와 함께 1만원이 놓여 있다고 가정

> 쪽지 내용
```
  배고프지?
  이걸로 밥 사먹어라
```

- 만약 쪽지가 없었다면?

  - 왜 돈이 식탁에 놓여 있는지, 누가 올려 둔 것인지, 무슨 용도인지 등 의문 발생

<br>

### 주석의 사용 예시
- 분명 과거의 내가 만든 코드인데 왜 이렇게 작성했는지 이해할 수 없는 경우

- 추가 설명이 필요한, 복잡한 코드를 작성한 경우

- 특별한 의미가 있는 어떤 값을 사용해야 하는 경우

- 다른 누군가와 함께 코드를 작성하여 서로 이해할 수 있게 부연 설명이 필요한 경우

<br>

> ch2.py
```
  name = "체다"  # 이름
  animal = "고양이"  # 종류
  age = 4  # 나이
  hobby = "낮잠"  # 취미

  # print("반려동물을 소개해 주세요.")
  """
  print("우리 집 반려동물은 " + animal + "인데, 이름이 " + name + "예요.")   # 종류, 이름
  print(name + "는 " + str(age) + "살이고, " + hobby + "을 아주 좋아해요.")  # 나이, 취미
  """
```
- print() 문은 소스 코드에서는 보이지만, 실행했을 때 아무 동작도 하지 않고 무시됨

<br>

> 실행결과
```
 
```

<br>

#### 💡 VSCode의 주석 단축키
- VSCode에서 주석을 단축키로 설정 가능

- 한 줄 전체를 주석 처리할 때

  - 문장 아무 곳에나 커서를 두고 아래 단축키 실행

    - 문장 일부만 주석 처리할 때는 단축키를 사용하기 어려우니 해당 내용 앞에 #를 직접 입력

- 여러 줄을 주석 처리할 때

  - 마우스 드래그 or 키보드 Shift + 방향키(↑, ↓)로 주석으로 지정할 영역을 선택한 뒤 아래 단축키 실행

    - \/(슬래시)는 키보드에서 숫자 키패드에 있는 키가 아니라 마침표 옆에 ?와 함께 있는 키

<br>

```
• 주석 설정 : Ctrl + / 또는 Ctrl + K + C (macOS일 때 command + / 또는 command + K + C )

• 주석 해제 : Ctrl + / 또는 Ctrl + K + U (macOS일 때 command + / 또는 command + K + U )
```

<br>

### 연습문제
#### ✏️ 1. 다음 코드의 실행결과로 올바른 것은?
```
  print("파이썬은") 
  # print("처음에는") 
  print("쉬워요")
```
```
  ① 실행결과
    파이썬은
  
  ② 실행결과
    처음에는
  
  ③ 실행결과
    파이썬은
    쉬워요
  
  ④ 실행결과
    파이썬은 
    처음에는
    쉬워요
```

<details>
  <summary>정답</summary>

<br>

> ③ 실행결과
```
    파이썬은
    쉬워요
```
```
  두 번째 print() 문은 주석 처리(#)됐으므로 실행결과에 표시 X
```

</details>

<br>
