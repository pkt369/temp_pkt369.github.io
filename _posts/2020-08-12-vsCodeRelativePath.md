---

layout : posts

title : "vsCode 상대경로 인식안됨"

date : 2020-08-12

categoris : devTool

comments : true

---

vscode에서 오류를 만났습니다. 하지만 상식선에서 쉽게 이해할수가 없었고, 그뒤 열심히 구글링을 해보았습니다.

하지만 구글링을 해도 원하는 결과가 나오지 않아 스스로 여러가지 방법을 시도해보게 되었습니다.

그러던 중 오류코드를 유심히 읽어보다가 ./가 상위 폴더를 향하고 있었습니다.

평소에 이클립스, visual studio 을 사용하다가 vscode로 넘어와서 생긴 오류였습니다.

openFolder 해서 열었던 폴더가 베이스였습니다.

예를 들어 openFolder가 **A**를 열었고 A 위에 있는 B폴더안에 c.js의 소스코드는

```javascript
//c.js
const fs = requrie('fs');

fs.openFile('./good.html')
```

이라고 하면 A 폴더에서 열었으므로 A 폴더가 상위폴더가 된니다. ./가 A인 셈입니다.

여기서 이클립스와 다른 점이보입니다. 이클립스는 ./만 써도 알아서 위의 폴더로 찾아가주지만 vscode에서는 직접 찾아가야합니다.

그래서 해결방법은 두가지 입니다.

**path함수 쓰기** :
코드로 설명드리겠습니다.

```javascript
const path = require('path');
const fs = require('fs');

const fs.openFile(path.join(__dirname, '/good.html'));
```

path.join함수와 __dirname을 통해 절대경로처럼 사용하실 수 있습니다.

두번째는 **openFile을 완전 상위폴더로 가기** 입니다.

B폴더를 openFolder를 통해 열면 ./가 제대로 원하던 상위 폴더를 가르키게 됩니다.
