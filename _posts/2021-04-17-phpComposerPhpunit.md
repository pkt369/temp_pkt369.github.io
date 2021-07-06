---

layout : posts

title : "Composer 을 통한 PHPUnit 사용하기"

date : 2021-04-17

categories : php

comments : true

---


PHP Unit은 PHP 코드 테스트 도구이며, 사실상 표준으로 자리를 잡았습니다.

PHP Unit을 설치하는 방법은 2가지가 있습니다.

1.  아카이브(phar 파일)을 다운로드하여 직접 실행하는 방법
2.  PHP 패키지 및 의존성 관리 도구인 컴포저(Composer)를 사용하는 방법


컴포저를 이용한 단위테스트 이기때문에 2번으로 진행하겠습니다.

<br>
<Br>

### 설치 방법
---
1.  composer 명령어로 PHP unit Test 설치
```
composer require --dev phpunit/phpunit
```
이렇게 명령어를 입력하면 현재 PHP 버전에 맞는 버전이 설치가 됩니다.
![PHPUnitVersion](https://user-images.githubusercontent.com/66049273/114971894-4690d500-9eb8-11eb-9f46-4c4ca18f1b5a.png)

<br>

2. 설치 확인
```
./vendor/bin/phpunit --version
```
<br>

3. 사용하기

use PHPUnit\Framework\TestCase; 를 추가하고 상속받아서 사용해야한다.
일단 폴더들은 이렇게 있다.
![test](https://user-images.githubusercontent.com/66049273/114972351-4ba25400-9eb9-11eb-8f9d-08bf3d726804.png)

/main/src/Util
```php
<?php  
namespace main\src;  
  
class Util  
{  
	  public function sum($a, $b) {  
		  return $a + $b;  
	  }  
  
	  public function minus($a, $b) {  
		  return $a - $b;  
	  }
}
```

test/src/SumTest
```php
<?php  
  
use PHPUnit\Framework\TestCase;  
use main\src\Util;  
  
class SumTest extends TestCase  
{  
	  public function testSum()  
	 {  
		  $a = 10;  
		  $b = 15;  
		  $sum = new Util();  
		  $testResult = $sum->sum($a, $b);  
		  $this->assertEquals($a + $b, $testResult);  
	 }  
}
```

돌리면 바로 잘나오는 것을 알수 있다.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3OTk1NDg0MzgsLTEzNzk1MjEwNTZdfQ
==
-->