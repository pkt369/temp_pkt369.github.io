---

layout : posts

title : "php version 바꾸기"

date : 2021-04-16

categoris : PHP

comments : true

---
﻿
php version 바꾸기
===
기존 회사에서 5.6 버전을 사용하다가 회사 내  app 개발을 위해서 7.3버전으로 넘어가야 했었습니다.

따라서 xampp를 다시 다운받고 여러가지설정들을 다시 해줘야 했습니다.

<br>

### phpstorm 내에서 설정
---
![phpstormSet1](https://user-images.githubusercontent.com/66049273/114963332-771c4300-9ea7-11eb-9ebf-4a23c623eba7.png)

php 버전을 변경을 제일 먼저 해주고, PHPUnit 을 사용하기 위해 CLI Interpreter 는 새로 설치한 xampp\php\php.exe 로 설정을 하여 사용을 했습니다.

참고) CLI(Command Line Interface) : 명령줄 인터페이스, 명령어 인터페이스, 주로 터미널을 생각하면 됩니다.

참고2) interpreter : 프로그래밍언어의 소스 코드를 바로 실행하는 것을 말한다. 반대로는 자바처럼 컴파일이 있다.

<br>
<br>

### 시스템환경설정
---
터미널을 사용할 때 php -v를 해보면 php 버전이 나오게 되는데 전 버전인 5.6 버전으로 나오고 있었습니다.

여러 설정들을 해보았지만 변경되지 않았었습니다. 
정답은 php에서 환경 설정하는 것이 아닌 윈도우에서 환경설정을 변경해줘야 됐었습니다.

  <br>

시스템 속성 → 고급 → 환경변수

안에 있는 Path 선택

![windowSet1](https://user-images.githubusercontent.com/66049273/114963548-f6aa1200-9ea7-11eb-8b35-91ca2c15b73e.png)

기존 : C:\xampp\php

변경후 : D:\xampp\php

![windowSet2](https://user-images.githubusercontent.com/66049273/114963596-0f1a2c80-9ea8-11eb-8c9e-7c52d81a34de.png)

이후 터미널에서 php -v를 하게 되었을 경우

![terminal](https://user-images.githubusercontent.com/66049273/114963627-1fcaa280-9ea8-11eb-9843-e99687926673.png)

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDAyNTIxNTI5XX0=
-->