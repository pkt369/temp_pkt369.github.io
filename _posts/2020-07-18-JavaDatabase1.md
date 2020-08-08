---

layout : posts

title : "자바 Database연동1"

date : 2020-07-18

categoris : Java

---

자바 프로젝트를 처음할 때 가장 힘들었던 것은 데이터 베이스와 연동해서 데이터를 주고 받는 것이었습니다.

그때의 기분을 살려서 조금더 자세히 포스팅 해볼려고 합니다.

첫편에서는 환경설정을 두번째편에서는 코드를 알아보려합니다.

먼저 데이터 베이스와 연동하기 위해서는
![ojdbc6](https://user-images.githubusercontent.com/66049273/87856713-d4588780-c95b-11ea-9721-5473794a52a2.png)

에 있는 **ojdbc6** 를 복사한후에


![ojdbc6_2](https://user-images.githubusercontent.com/66049273/87856725-e9cdb180-c95b-11ea-9bfd-265bf63ba5ec.png)

로 복사해주셔서 ojdbc6가 이클립스의 `Jre System Library`에 들어가도록 해주세요.

그리고 물론 데이터베이스가 먼저 설치되어 있으셔야 합니다.

![tool](https://user-images.githubusercontent.com/66049273/87856885-2c43be00-c95d-11ea-8d2e-671d296b0d5a.png)

그런다음 이미지와 같이 `Data Source Explorer`을 Open해주세요.

![data1](https://user-images.githubusercontent.com/66049273/87856979-f226ec00-c95d-11ea-8fdb-cf90de8ab56d.png)

그런다음 오른쪽마우스키를 눌러서 New를 해주세요.

![data2](https://user-images.githubusercontent.com/66049273/87856980-f2bf8280-c95d-11ea-8b7b-e6eef54c8923.png)

저는 오라클을 사용하기때문에 오라클을 기준으로 하겠습니다.  

Next를 눌러줍시다.

![data3](https://user-images.githubusercontent.com/66049273/87856981-f3581900-c95d-11ea-890a-fd678b67043c.png)

를 눌러 새로운 드라이버 정의를 해주세요.

![data4](https://user-images.githubusercontent.com/66049273/87856982-f3f0af80-c95d-11ea-87c2-1ab8bf38a8ca.png)

저같은 경우 Oracle Thin Driver 11입니다.

그다음 **JAR List** 를 눌러주세요.(Name/Type옆에)

그리고 **Add JAR/Zip..** 눌러주세요.

그럼파일을 선택하라고 나올텐데 제가 올린  첫번째 사진의 주소로 들어가주세요.

**C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib**

![data5](https://user-images.githubusercontent.com/66049273/87857186-b2610400-c95f-11ea-9542-9fcabaf30b71.png)

그리고 `ojdbc14.jar`을 삭제해주세요.

그다음 Properties를 눌러주세요.

![data6](https://user-images.githubusercontent.com/66049273/87857187-b2610400-c95f-11ea-8ab4-ae8e1869e6cb.png)

적힌대로 써주세요. 설명을 조금 도와드리면

**url : [DBMS이름] @ [주소] : [포트] : [데이터베이스 식별자]** 입니다.

그리고 데이터베이스 id와 passwd를 입력해주세요.

![data7](https://user-images.githubusercontent.com/66049273/87857184-b12fd700-c95f-11ea-8219-f74cd862d4a7.png)

그다음 확인을 누르고 여기 이미지와 같이 보이신다면 Test Connection을 눌러서

![data8](https://user-images.githubusercontent.com/66049273/87857324-dec95000-c960-11ea-8e2a-14638cba7a94.png)

를 눌러서 잘되었는지 확인을 해줍시다.

그다음 연결이 되어있는지 확인해줍니다.

만약 밑에 사진과 되어있지 않다면 다시 `New Oracle`에 오른쪽키를 눌러서 `connect`를 눌러줍시다.


![데이터베이스연결](https://user-images.githubusercontent.com/66049273/87856315-53988c00-c959-11ea-940d-d17970bdfe41.png)

이런식으로 되어 있다면 연동 성공입니다.

그리고 여기서 조금 더확인을 하고 싶으신 분은
**File-New-Other** 를 누르셔서

![sql1](https://user-images.githubusercontent.com/66049273/87857442-a0806080-c961-11ea-84e5-938b196cbd27.png)

SQL 파일을 생성해주신다음

![sql2](https://user-images.githubusercontent.com/66049273/87857441-9f4f3380-c961-11ea-8a29-2512d6380850.png)

이미지와 같이 연동을 해주신다음 데이터베이스언어로 바로 실행시켜봅니다.

실행하고 싶은 문장을 드래그해서 **Alt+X** 를 눌러 개별실행을 시켜줍니다.

다음 포스팅에서는 코드편으로 돌아오겠습니다.
