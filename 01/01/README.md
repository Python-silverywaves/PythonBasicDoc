# 개발환경 설정
개발환경 설정이란
---
- 프로그래밍 언어로 프로그램을 작성할 때 필요한 준비 과정

  - 사용하는 PC의 운영체제 또는 프로그래밍 언어에 따라 다양
 
  - 본인에게 가장 편하거나 익숙한 도구를 이용

<br>

#### 💡 Note 개발 환경 설정 시 내 화면과 다르다면?
```
  프로그램마다 새로운 버전이 나오면 환경 설정 방법이 조금씩 달라질 수 있음
  
  사용하는 PC의 운영체제가 macOS 인지 Windows 인지에 따라서도 달라짐
```
- [Windows 설정](https://nadocoding.tistory.com/4)

- [macOS 설정](https://nadocoding.tistory.com/101)

<br>

---

<br>

파이썬 설치
---
### 1. [파이썬 다운로드 페이지](https://www.python.org/downloads) 접속
- 화면을 아래로 스크롤

  - Looking for a specific release? : 파이썬의 전체 버전을 보여 줌

  - 원하는 버전의 Download 버튼을 찾아 클릭

#### 📌 Tip
```
  파이썬 공식 홈페이지에서는 다양한 버전을 제공

  최신 버전은 일부 패키지가 제대로 작동하지 않을 수 있기 때문에 예전 버전 사용 경우 多
```

<br>

### 2. 스크롤 내려 Files 항목에서 운영체제에 맞는 버전 선택
- 윈도우 기준 Windows x86 executable installer 다운로드 진행

<br>

### 3. 내려받은 파일을 클릭해 실행
- Add Python 3.8 to PATH 옵션 체크

- Customize installation

<br>

### 4. 옵션 선택 화면이 보이면 기본값을 그대로 둔 상태로 Next

<br>

### 5. 설치 경로를 나타내는 Customize install location 입력란에 C:\Python{버전}
- ex) 버전이 3.10이면 Python310, 버전이 3.12면 Python312

#### 📌 Tip
```
  설치 경로에서 폴더명 앞에 있는 역슬래시(\)는 키보드에서 ₩(원화 기호)와 같은 키
```

<br>

### 6. 설치가 끝나면 Close 버튼을 눌러 설치 프로그램을 종료

<br>

---

<br>

비주얼 스튜디오 코드 설치
---
- 프로그래밍 언어로 프로그램을 개발하려면 코드 작성을 돕는 텍스트 편집기 또는 에디터(editor) 필요

  - VSCode는 다양한 프로그래밍 언어를 개발할 수 있는 강력한 도구
 
  - 다른 언어를 공부할 때도 새로운 개발 환경에 적응하는 과정 없이 바로 학습할 수 있음

<br>

#### 💡 파이썬 에디터
```
  파이썬에서 사용할 수 있는 유용한 에디터
  
  버전이 변경되는 경우가 있을 수 있으므로 사용 방법은 아래 링크 참고
```
- [파이참(PyCharm)](https://nadocoding.tistory.com/102)

- [Rep.it](https://nadocoding.tistory.com/103)

- [주피터 노트북(Jupyter Notebook)](https://nadocoding.tistory.com/104)

- [구글 코랩(Google Colab)](https://nadocoding.tistory.com/105)

<br>

### 1. [VSCode](https://code.visualstudio.com) 접속
- Download for Windows 다운로드

#### 📌 Tip
```
  운영체제가 다르다면 Download for Windows 버튼 옆에 ▾ 클릭 후 운영체제에 맞는 버전을 선택
```

<br>

### 2. 내려받은 파일 실행
- 사용권 계약 화면에서 '동의합니다' 옵션을 선택하고 '다음'

<br>

### 3. 설치 위치와 시작 메뉴 폴더 선택 화면이 순서대로 나오면 기본값을 그대로 두고 '다음'

<br>

### 4. 바탕 화면에 바로가기 만들기 옵션을 선택하고 '다음'

<br>

### 5. 설치 버튼을 클릭해 VSCode를 설치 후 종료

<br>

VSCode 설정
---
### 1. 컴퓨터 바탕화면에 PythonWorkspace 폴더 생성

<br>

### 2. VSCode 실행시 화면 왼쪽에 있는 액티비티 바(activity bar)에서 첫 번째 메뉴인 탐색기(Explorer) 클릭

<br>

### 3. 사이드 바(side bar)가 열리면서 메뉴 노출
- NO FOLDER OPENED(열린 폴더 없음)에 있는 Open Folder(폴더 열기) 버튼을 클릭

<br>

### 4. 폴더 선택 창이 열리면 바탕화면에 있는 PythonWorkspace 폴더를 찾아 선택

#### 📌 Tip
```
  폴더를 선택하고 나면 폴더의 파일 작성자를 신뢰하는지 묻는 창 나타남

  신뢰한다는 의미로 체크박스에 표시하고 Yes, I trust the authors 버튼 클릭
```

<br>

### 5. 사이드 바에 PythonWorkspace 폴더가 표시
- 폴더명 위에 마우스를 가져가면 나타나는 아이콘들 중 New File(새 파일) 클릭

<br>

### 6. 입력란이 나오면 helloworld.py를 입력하고 Enter
- helloworld.py

  - helloworld : 파일명
  
  - 점(.) : 구분 기호
  
  - py : 확장자
 
    - 확장자 위치에 py를 넣으면 파이썬 소스 파일, c라고 넣으면 C 언어 소스 파일

<br>

### 7. 화면 오른쪽에 helloworld.py 파일 오픈
- 아래쪽에 팝업창이 나타나면 Install 버튼을 클릭해 설치

- 팝업창이 나타나지 않는다면 직접 확장 프로그램을 찾아 설치

  - 왼쪽 액티비티 바에서 다섯 번째 메뉴인 확장 프로그램(Extensions)을 클릭
 
  - 사이드 바가 열리고 검색창이 보이면 python을 입력하고 Enter
 
  - 검색 결과에서 Python 확장 프로그램이 보이면 Install(설치) 버튼을 클릭해 설치

<br>

#### 💡 확장 프로그램
```
  VSCode는 다양한 언어로 코드를 작성할 수 있는 에디터이므로 
  한 프로그래밍 언어를 선택해 코드를 작성하려면 해당 언어를 VSCode와 연동할 수 있는 확장 프로그램을 설치해야 함
  
  확장자에 따라 파일 탐색기에 보이는 파일명에 아이콘을 붙여 예쁘게 보여주는 확장 프로그램,
  소스 코드의 시작과 끝을 한눈에 볼 수 있게 해 주는 확장 프로그램 등
  조금 더 편하게 개발하기 위한 확장 프로그램도 있음
  
  이런 프로그램들은 사용자 개개인에 최적화한 환경을 구성할 수 있게 도와주지만
  개인마다 호불호가 있고 본인만의 개발 스타일에 따라 필요한 프로그램이 달라질 수도 있어
  구글에서 ‘VSCode 확장 프로그램’ 또는 ‘VSCode Extension’으로 검색해 스타일에 맞는 것 설치하면 됨
```

<br>

### 8. 설치가 끝나면 컴퓨터에 설치된 파이썬 버전이 화면 아래 상태 바에 표시
- 버전 부분을 클릭하면 컴퓨터에 설치된 파이썬 버전 목록이 나타나고, 원하는 버전 선택하면 해당 버전으로 변경

<br>

#### 💡 VSCode 테마 선택
```
  VSCode는 어두운 테마(dark)를 기본으로 제공
  
  테마를 바꾸고 싶다면? 
    1. 메뉴에서 File(파일) → Preferences(기본 설정) → Theme(테마) → Color Theme(색 테마) 선택
    2. 단축키로 Ctrl + K + T (macOS일 때 command + K + T)
```

<br>
