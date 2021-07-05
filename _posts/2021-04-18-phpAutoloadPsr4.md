---

layout : posts

title : "autoload (psr-4)"

date : 2021-04-18

categoris : php

comments : true

---

세팅을 다하고나서 파일이 불러오지 않아서 어떤 이유인지 알아봤습니다.

문제는 namespace를 잘못 이해를 했기 때문인데 namespace는 자바처럼 상위폴더부터 적는게 아니라 절대 루트처럼 적어줘야했기 때문입니다.

예) \_\_DIR\_\_ . "/src/lib/Util.php";

모든 파일들을 하나씩 추가하다보면 관리하기 어렵고 오타로 인한 실수가 발생할 수 있습니다.

<br>

autoload를 통해 단 한줄만 추가하면 편리하게 자바처럼 파일을 가져와 사용할 수 있습니다.

```php
require_once 'vendor/autoload.php';
```
<br>
<br>

### PSR-4 자동 로딩 설정
---
먼저 composer.json을 편집하여 사용하기 때문에 먼저 만들어 둬야 합니다.
```json
"autoload"  : {
	"psr-4"  : {
		"App\\"  : "app/"
	}
}
```

먼저 composer.json 에는 오토로드의 psr-4 를 먼저 만들어주고
```
composer dump-autoload
```
를 입력하면

vender/composer/autoload_psr4.php 에 자동으로 루트가 생성이 됩니다.

![autoload](https://user-images.githubusercontent.com/66049273/114973745-04699280-9ebc-11eb-82c2-9c1542fb79a3.png)
![autoload2](https://user-images.githubusercontent.com/66049273/114973811-282cd880-9ebc-11eb-9a6a-cc3d97d3cedd.png)

결론적으로 namespace를 제대로 이해하지 못해서 생긴 사건같습니다.

조금더 정리를 해보자면 namespace는 루트부터 적어도 자바처럼 작동하지 않는다는 것입니다.

<br>  

두번째로 namespace를 제대로 사용하기 위해서는 \_\_DIR__ . src~ 이런식으로 dir을 써줘야 합니다.

  <br>

매번 이렇게 적기 힘들기때문에 autoload를 사용하는데 autoload는 설정해놓은 루트에 접근하면 자동으로 루트(절대 경로)를 더해서 접근해주는 역할인것입니다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MDkzOTAxMzksLTExOTcxMzgzNjZdfQ
==
-->