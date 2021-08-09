---
layout : posts

title : "젠킨스란 무엇인가"

date : 2021-07-29

categories : java

comments : true
---



새로운 프로젝트에 제킨스를 적용하기 위해서 알아보았다.

### 원인 및 과정

회사에서 코드를 리팩토링을 진행하여 상품을 많이 업로드할 수 있도록 만들었다.

업로드할때 시간은 엄청 줄었지만 렌더링할때 오래걸리고 버벅거리는 증상이 발현했다.

어디서 버벅거리는지 알기위해서 크롬의 Performance를 이용했다. 크롬의 Performance는 개발자 도구(f12)의 탭에서 선택할 수 있다.

![performance](https://user-images.githubusercontent.com/66049273/128444983-5c7a69df-545d-4cae-838b-dfa2ef2f591d.png)



#### 첫번째 원인 : 많은 옵션 + select2

select2는 검색 기능을 가진 select태그이다. 

![select2Search](https://user-images.githubusercontent.com/66049273/128450468-d1293817-276e-47cf-852e-f341994d5ccd.png)

크롬의 Peformance의 call Tree 쪽을 보면 함수 영역이 99프로를 차지한다고 나오는데 계속 파고들어가면

![performance2](https://user-images.githubusercontent.com/66049273/128450517-1644f706-aa5d-48db-81f0-538038b51c95.png)

select2에서 옵션을 생성하느라 엄청 많은 양의 시간을 잡아 먹는것을 볼수 있다. 한 품목당 한개당 800개와 900개 총 두개의 select를 가지는데 600개를 렌더링하게되면 1700 * 600 = 1,020,000 으로 엄청 많은 양의 옵션을 생성한다.

그래서 해결방법으로 select2에 있는 ajax 지연 렌더링을 사용했다. 지연 렌더링을 사용하면 800개의 옵션 중 10개만 불러오고 스크롤을 내리면 더 가져오는 방식이다.

![lazyloading](https://user-images.githubusercontent.com/66049273/128450554-3d2af1a6-30ff-4179-b4de-e252e28cc6e3.png)



![performance2](https://user-images.githubusercontent.com/66049273/128450574-e7a37a72-06d8-47ea-b8d0-7a1f6be4d172.png)

지연 렌더링 이후에도 많은 시간이 걸리고 있었다.



지연 렌더링을 시켰지만 여전히 많은 시간이 아직도 select2에서 소비되고 있었다. 그다음으로 시도해보았던 것이 select2를 대체할 choice js를 사용해보는 것이었다.

choice js는 오픈소스로 제이쿼리대신 자바스크립트를 사용해 select2보다 성능이 좋다고 알려져 있었다. 하지만 사용해본 결과 choice js 가 select2보다 더 버벅거림이 심했다.

![choicejs](https://user-images.githubusercontent.com/66049273/128450612-55d99c7f-deba-409e-85ed-9e1e6fecc1fb.png)

참고 ) 100개 검색



그래서 다시 select2로 돌아올수 밖에 없었고, 다른 방법을 모색했다. 다른 방법으로 떠올린 것은 초기에 select2를 렌더링하지 않는 것이다.

마우스를 오버했을때만 select2를 사용하도록 변경하는 것이었다.

![image](https://user-images.githubusercontent.com/66049273/128450662-cb401f32-b98f-499a-a6bd-94bf2e6de622.png)

