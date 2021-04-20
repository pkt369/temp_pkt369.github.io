---

layout : posts

title : "컴포저 아카이브 사용법"

date : 2021-04-16

categoris : PHP

comments : true

---
﻿

컴포저는 PHP 소프트웨어와 필요 라이브러리의 의존성을 관리하기 위한 표준 포맷을 제공하는 패키지 관리자를 뜻한다.

  
<br>
<br>

### 패키지 셋업
---
프로젝트에서 사용하기 위해서는 'composer.json'을 사용하고 json 포맷으로 작성합니다.

require 키를 이용해 필요한 패키지를 가져올수 있고, 패키지 이름과 패키지 버전을 맵핑하여 사용합니다.

```json
{
	"require": {
		"monolog/monolog": "1.0.*"
	}
}
```
패키지 이름은 벤더의 이름과 프로젝트의 이름으로 구성되어 있고, 예를들어 igorw/json , phpst/json 으로 만들 수 있습니다.

벤더는 패키지의 충돌을 방지하기위해 사용합니다.

<br>
<br>

### 패키지 설치
---
의존관계가 선언된 패키지들을 로컬 프로젝트로 다운하기 위해서 composer.phar의 install 명령을 입력하여 사용합니다.
```
php composer.phar 

> Blockquote

install
```
이 명령어를 입력하면 위에서 설치한 monolog/monolog 패키지의 매칭되는 가장 최신버전을 vendor 디렉토리에 다운로드받습니다.

vendor 는 서드파티의 패키지들이 다운로드 되는 폴더를 의미합니다.

위에 monolog 경우 vendor/monolog/monolog에 다운로드 됩니다. (참고 : 깃에 서드파티의 코드가 추가되길 원하지않으면 .gitignore에 추가하여 사용하기)

install 명령어를 통해서 의존관계가 설정된 패키지들 설치한 후에는 composer.lock파일이 프로젝트 루트 디렉토리에 생성됩니다.

<br>
<br>

### Composer.lock - 잠금 설정 파일
---
의존성 패키지들을 설치한 뒤에 컴포저는 composer.lock파일에 설치한 패키지들의 정확 버전 목록을 저장합니다.

이 장금 설정들이 프로젝트가 필요로 하는 특정 버전을 의미합니다.

<br>

설치 순서 : install 명령어 → composer.lock 존재 확인 → 있다면 composer.json에 관계없이 장금설정된 버전의 패키지들을 다운로드

이런 순서를 가지는 것의 장점은 프로젝트를 셋업하고 의존성 패키지들을 다운로드 하려고하는 어떤 누구라도 동일한 버전의 의존 패키지를 다운받음으로써 버전이 안맞음으로써 생기는 버그를 애초에 막을 수 있다.

  
<br>
composer.lock이 없다면 composer.json 으로부터 의존성과 버전 정보를 읽어 들여 update 명령어 또는 install 명령어가 실행 된 이후 lock 파일을 생성합니다.

이말은 새로운 버전이 나오더라도 자동으로 업데이트 되진 않아서 update 명령어를 통해 최신 패키지를 다운받아야한다.
```
php composer.phar update

php composer.phar update monolog/monolog [...]
```

<br>
<br>

### Packagist - 패키지스트
---
Packagist는 컴포저 저장소이며, 패키지스트에 올라와 있는 모든 패키지들을 require 할수 있다.

[packagist.org](http://packagist.org/) 에서 패키지들에 대해서 검색하여 정보를 얻을 수 있다.

<br>
<br>

###  Autoloading - 오토로딩
---
컴포저는 라이브러리들에 대한 오토로딩 정보를 vendor/autoload.php 파일에 저장합니다. 이 파일을 include 하여 오토로딩을 쉽게 사용할수 있습니다.
```
require 'vendor/autoload.php';
```
이렇게하여 서드파티의 코드를 사용을 쉽게합니다. 예를 들어 작성하고 있는 프로젝트가 monolog에 의존성을 가지고 있을때 오토로딩을 사용하면 바로 해당 클래스를 사용할 수 있습니다.

<br>

오토로딩의 설정은 composer.json의 autoload 설정을 통해서도 할 수 있습니다.
보통 요즘은 psr-4를 많이 이용한다고 합니다.
```json
{
	"autoload": {
		"psr-4": {"Acme\\": "src/"}
	}
}
```

Acme 네임스페이스를 psr-4에 따라서 오토로딩을 설정합니다. 오토로딩은 네임스페이스에 대한 디렉토리 매핑을 정의합니다.

src 디렉토리는 vendor 디렉토리와 마찬가지로 프로젝트 루트 디렉토리에 존재합니다. 예를 들어 src/Foo.php 파일은 Acme\Foo 클래스를 의미합니다.

  
<br>
autoload 항목을 추가한 뒤에는 dump-autoload 명령어를 실행하여 vendor/autoload.php 파일을 재성성 해줘야합니다.

autoload.php 파일을 include하게 되면 오토로더 인스턴스를 리턴받을 수 있습니다. 이 리턴 받은 인스턴스를 통해 추가적인 네임스페이스를 지정할 수도 있습니다.

예를 들어 테스트가 필요한 경우 다음처럼 사용할수 있습니다.
<br>
```
$loader = require 'vendor/autoload.php';
$loader->add('Acme\\Test\\', __DIR__);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM1OTM1NDQwMyw2MjgwODQxNjBdfQ==
-->