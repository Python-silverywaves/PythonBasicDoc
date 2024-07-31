# 실습 문제: 부동산 프로그램 만들기
주어진 코드를 활용해 부동산 프로그램을 작성
---
### 조건
- 생성자로 인스턴스 변수를 정의
  - 매물 정보를 표시하는 show_detail() 메서드에서는 인스턴스 변수를 순서대로 출력

- 실행결과에 나온 3가지 매물을 객체로 만들고 총 매물 수를 출력한 뒤 show_detail() 메서드를 호출해 각 매물 정보를 표시

```
  class House:
      # 매물 초기화: 위치, 건물 종류, 매물 종류, 가격, 준공연도
      def __init__(self, location, house_type, deal_type, price, completion_year):
          pass
  
      # 매물 정보 표시
      def show_detail(self):
          pass
```

<br>

> 실행결과
```
  총 3가지 매물이 있습니다.
  강남 아파트 매매 10억 원 2010년
  마포 오피스텔 전세 5억 원 2007년
  송파 빌라 월세 500/50만 원 2000년
```

<br>

<details>
  <summary>정답</summary>

<br>

> 코드
```
  class House:
      # 매물 초기화: 위치, 건물 종류, 매물 종류, 가격, 준공연도
      def __init__(self, location, house_type, deal_type, price, completion_year):
          self.location = location
          self.house_type = house_type
          self.deal_type = deal_type
          self.price = price
          self.completion_year = completion_year
      # 매물 정보 표시
      def show_detail(self):
          print(self.location, self.house_type, self.deal_type, \
              self.price, self.completion_year)
  
  houses = []
  house1 = House("강남", "아파트", "매매", "10억 원", "2010년")
  house2 = House("마포", "오피스텔", "전세", "5억 원", "2007년")
  house3 = House("송파", "빌라", "월세", "500/50만 원", "2000년")
  
  houses.append(house1)
  houses.append(house2)
  houses.append(house3)
  
  print("총 {0}가지 매물이 있습니다.".format(len(houses)))
  for house in houses:
      house.show_detail()
```

<br>

> 실행결과
```
  총 3가지 매물이 있습니다.
  강남 아파트 매매 10억 원 2010년
  마포 오피스텔 전세 5억 원 2007년
  송파 빌라 월세 500/50만 원 2000년
```

<br>

> 1. House 클래스의 생성자는 전달값에 넘어온 값들로 인스턴스 변수를 생성(앞에 self. 붙여야 함)

<br>

> 2. show_detail() 메서드는 특별한 내용 필요 X → print() 문으로 인스턴스 변수를 순서대로 출력
```
  class House:
      # 매물 초기화: 위치, 건물 종류, 매물 종류, 가격, 준공연도
  ➊ self.을 붙여 인스턴스 변수 정의
      def __init__(self, location, house_type, deal_type, price, completion_year):
          self.location = location
          self.house_type = house_type
          self.deal_type = deal_type
          self.price = price
          self.completion_year = completion_year
      # 매물 정보 표시
      def show_detail(self):
          print(self.location, self.house_type, self.deal_type,\
              self.price, self.completion_year) ---- ➋ 인스턴스 변수의 값 순서대로 출력
```

<br>

> 3. 여러 매물을 관리해야 하므로 houses라는 이름으로 리스트 생성
> > 리스트에 추가될 매물 정보가 준비되지 않았으므로 값이 없는 빈 상태로 정의

<br>

> 4. House 클래스로 각 매물 정보를 전달해 객체 3개를 생성

<br>

> 5. 생성한 객체들을 append() 함수로 houses 리스트에 추가

<br>

```
  houses = []---- ➌ houses 리스트 생성
  ➍ House 클래스로 객체 3개 생성
  house1 = House("강남", "아파트", "매매", "10억 원", "2010년")
  house2 = House("마포", "오피스텔", "전세", "5억 원", "2007년")
  house3 = House("송파", "빌라", "월세", "500/50만 원", "2000년")
   
  
  ➎ houses 리스트에 객체 추가
  houses.append(house1)
  houses.append(house2)
  houses.append(house3)
```

<br>

> 6. 총 매물 수를 출력해야 하므로 print() 문 작성
> > 각 매물은 houses 리스트에 객체로 저장 → houses 리스트의 객체 개수 = 총 매물 수 <br>
> > 문자열의 길이를 확인할 때 사용한 len() 함수로 리스트의 길이도 확인 가능

<br>

```
  print("총 {0}가지 매물이 있습니다.".format(len(houses))) ---- ➏ 총 매물 수 출력
```

<br>

> 7. 각 매물의 정보를 표시하기 위해 객체별로 show_detail() 메서드 호출
> > 객체는 리스트로 관리 → 반복문을 사용 → 같은 코드 반복 작성 X, 짧은 코드로 원하는 동작 구현 가능

<br>

```
  for house in houses: ---- ➐ 반복문으로 매물 정보 출력
      house.show_detail()
```

</details>

<br>
