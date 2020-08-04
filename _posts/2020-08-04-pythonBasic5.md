---

layout : posts

title : "파이썬 기본 문법5(모듈, 패키지)"

date : 2020-08-04

categoris : Python

comments : true

---

파이썬 기본문법 시리즈 5편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)

<h4>모듈(Module)</h4>

- 사전적 의미 : 독자적인 기능을 갖는 구성 요소
- 파이썬에서는 각각의 소스 파일을 일컬음
- 제공자 기준
  - 표준 모듈 : 파이썬과 함께 제공되는 모듈
  - 사용자 생성 모듈 : 프로그래머가 직접 작성한 모듈
  - 서드 파티 모듈 : 다른 프로그래머 or 업체에서 제공한 모듈

<br>

**import**
- 다른 모듈을 현재 모듈로 불러오는 기능
- '다른 모듈 내의 코드에 대한 접근'을 가능
- 접근 가능 코드는 변수/함수/클래스 모두 포함

<br>


**사용방법**
- import 모듈명
- from 모듈명 import 변수 또는 함수

exam)
- import math
- from calculator import plus(calculator는 임시로 만든 것)

<br>


**모듈(Module) 경로 탐색 규칙**
- import문을 만나
  - 파이썬 인터프리터 내장 모듈 검색(sys.builtin_module_name)
- sys.path에 정의되어 있는 디렉토리 검색
  - 파이썬 모듈이 실행되고 있는 현재 디렉토리
  - PYTHONPATH 환경변수에 정의되어 있는 디렉토리
  - 파이썬과 함께 설치된 기본 라이브러리

<br>

**메인 모듈(Main Module)**
- 별도의 메인 함수가 따로 없음.
- '최상위 수준(Top Level)'에서 실행되는 스크립트만 있다.
- 최상위 수준 실행 -> 명령 프롬프트 창이나 탐색기를 이용하여 파이썬 모듈을 실행하는 것을 말함.
- 메인모듈 : 최상위 수준으로 실행되는 스크립트
- `__name__` : 내장 전역 변수, 모듈이 최상위 수준으로 실행 될 때 `__main__`으로 지정됨.

<br>

**하위 모듈(Sub Module)**
- 메인 모듈이 import문을 이용하여 불러오는 모듈
- `__name__` : 모듈 자체의 이름을 담고 있음.

<br>

**패키지(Package)**
- 모듈을 모아놓는 디렉토리
- 해당 디렉토리가 파이썬의 패키지로 인식되려면 `__init__.py`파일을 그 경로에 가지고 있어야 함.
- `__init__.py`
  - `__all__`변수 조정 : 패키지로 부터 반입할 모듈의 목록을 정의하기 위해 사용

<br>

파이썬의 기본 라이브러리 패키지 외에 추가적인 패키지를 설치하는 디렉토리 :

```python
>>>import sys
>>>sys.path
['C:\\workspaces\\sources\\python\\chap07\\main_sub2',
…
, 'C:\\Anaconda3\\envs\\venvModel\\lib\\site-packages',
…
,'C:\\Anaconda3\\envs\\venvModel\\lib\\site-packages\\Pythonwin']
>>>from my_package import my_module
>>>my_module.info()
```

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
