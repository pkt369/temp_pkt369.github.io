---
layout : posts

title : "git Token Login(토큰인증 로그인)"

date : 2021-08-16

categories : java

comments : true
---



최근에 git 에서 8월 13일 이후로는 패스워드로 push 가 안되고 있었다. 필자도 블로그를 작성했는데 푸쉬가 안되어서 정말 놀랐었다. 그래서 이번에는 패스워드 대신 토큰인증으로 push 를 하는 것을 알아보자.

<br>

### 오류

------

`remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead. ... The requested URL returned error: 403`

git 에서 비밀번호를 토큰으로 대체하라는 메세지가 나오면서 403오류를 리턴해주고 있다.

<br>

### 토큰 생성하기

------

git 에서 먼저 토큰을 발급받아야 한다. git에서 오른쪽위 아이콘을 누르고 Settings를 눌러준다.

![settings](https://user-images.githubusercontent.com/66049273/129469608-cbfdb1ef-db33-4357-a63a-2ff43a101b0f.png)

<br>

이후 developer Settings를 눌러준다.

![developer settings](https://user-images.githubusercontent.com/66049273/129469624-c33cc28a-8dfb-47d5-bedc-0f6fad4c5e40.png)

<br>

이후 **Personal access tokens**를 누르고 **Generate new Token**을 누른다.

![generate new token](https://user-images.githubusercontent.com/66049273/129469655-e02943c0-de53-4fb7-a337-cf06547926b4.png)

<br>

그리고 Note 에 어떤 토큰인지 적고 repo를 체크해주고 토큰을 생성해준다.

![loginToken생성방법](https://user-images.githubusercontent.com/66049273/129469688-cb523ab9-274f-4938-81d4-3739d42c8783.png)

<br>

그러면 이렇게 토큰 정보가 나오는데 **한번만 나오기때문에 반드시 다른곳에 따로 저장을 해놓아야한다!**

![tokenCheck](https://user-images.githubusercontent.com/66049273/129469702-1e11b7ae-eb2f-496b-a83b-66881d5a1c7a.png)

<br>

### 자격증명에서 비밀번호에서 토큰으로 변경

------

제어판 -> 사용자 계정 -> 자격 증명 관리자로 이동 후 Windows 자격 증명 클릭

![window 자격증명](https://user-images.githubusercontent.com/66049273/129469783-e70ea8b1-e29f-4c30-8801-24da340d7f76.png)

<br>

밑의 사진처럼 편집을 클릭

![자격증명편집1](https://user-images.githubusercontent.com/66049273/129469854-65ad1c6b-8318-40c0-814e-f9be6fded0c8.png)

<br>

이전에 받았던 토큰을 붙여넣고 저장을 눌러주면 끝이다.![자격증명편집2](https://user-images.githubusercontent.com/66049273/129469865-7cf01115-34d1-4dc8-b82b-11a6bd3cd42b.png)

<br>

이후 푸쉬해보면 정상적으로 잘되고 있는 것을 볼수 있다.
