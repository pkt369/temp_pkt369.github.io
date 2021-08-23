---
layout : posts

title : "젠킨스 git push 시 자동 빌드하기"

date : 2021-08-23

categories : java

comments : true
---



이전 포스팅에서 젠킨스 git 연동하기를 포스팅하였으므로 이미 git 연동이 되었다는 가정하에 포스팅하겠습니다.

<br>

### Webhook

앱 to 앱으로 실시간 정보를 제공하는 방법. web callback, HTTP push API, 역방향 API 라고 할수 있다.

전형적인 API는 실시간 데이터를 가져올려면 자주 호출해야하는 단점이 있지만, 이방식을 사용하면 즉시 데이터를 얻을수 있다.

필자는 gradle 을 사용한 스프링 부트 프로젝트를 연동하였으니 참고 바란다.

<br>

#### Webhook 추가하기

본인의 프로젝트의 GitHub 프로젝트 Settings -> Webhooks -> Add Webhook 클릭

![addWebhook](https://user-images.githubusercontent.com/66049273/130433711-966743f5-72a5-43f8-9fa9-8595597814bb.png)

<br>

Payload URL 에는 "http://젠킨스 주소/github-webhook/"을 넣어준다.

참조) 외부에서 접근이 가능하도록 방화벽 설정이 열려있어야 한다. 필자의 경우 aws의 ec2 에서 jenkins를 설치하였으므로, 다음 ip를 추가하면 된다.

```
192.30.252.0/22
185.199.108.0/22
140.82.112.0/20
```

참조) https://api.github.com/meta 에서 hooks를 보면 될것

<br>

그리고 나머지는 기본으로 두고 Add Webhook을 클릭하면 된다.

![Webhooks](https://user-images.githubusercontent.com/66049273/130434668-fb8105de-aeac-4d03-95f9-3fc67145d8d5.png)

<br>

#### Github Integration Plugin 설치하기

git 과 jenkins를 연결 시켜주는 것이 Github Integration Plugin이며, Jenkins 관리 -> 플러그인 관리에 있다.

![github Integration](https://user-images.githubusercontent.com/66049273/130434990-f3704fe8-171b-4ed5-81e1-aaaad1690c1a.png)

필자는 이미 설치가 되어서 설치된 플러그인에 있다는 것을 참고하기 바란다.

<br>

#### 젠킨스 설정

이전 포스팅에서 생성한 item을 클릭 -> 구성 클릭

![gotoProject](https://user-images.githubusercontent.com/66049273/130435475-1cd63392-d32b-4011-a88f-b4453b71563f.png)



이후 빌드 유발을 클릭한 후 `GitHub hook trigger for GITScm polling`을 체크 한 후 저장

![빌드유발](https://user-images.githubusercontent.com/66049273/130435737-097ac9a5-4780-4318-bd4a-501ed90504c3.png)



여기까지 따라왔다면 설정이 완료된 것이다. 이제부터는 branch 에 push를 하면 자동으로 jenkins 빌드가 실행이 된다.

<br>

<br>

#### Reference

https://goddaehee.tistory.com/260

