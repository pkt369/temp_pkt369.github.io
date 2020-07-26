---

layout : posts

title : "R 정형 비정형2"

date : 2020-07-28

categoris : R

---

R 정형 비정형 시리즈 2편입니다.

R 정형 비정형 시리즈 전편은 [R 정형 비정형 시리즈 1편](https://pkt369.github.io/R_Structured1)로 들어가시면 됩니다.

**단어구름에 디자인 적용(빈도수, 색상, 랜덤, 회전 등)**

`d <- data.frame(word=myName, freq=wordv)`

`str(d)`

색상 지정  

`pal <- brewer.pal(12,"Paired")` # Set1~Set3

폰트 설정세팅 : "맑은 고딕", "서울남산체 B"  
`windowsFonts(malgun=windowsFont("맑은 고딕"))` #windows

색상, 빈도수, 글꼴, 회전 등 적용  
`wordcloud(d$word, d$freq, scale=c(5,1), min.freq=3, random.order=F, rot.per=.1,
colors=pal, family="malgun")`

wordcloud(단어, 빈도수, 5:1비율 크기,최소빈도수,랜덤순서,회전비율, 색상(파렛트),컬러,글꼴 )

ex) ![wordcloud2](https://user-images.githubusercontent.com/66049273/88483602-d6e25f00-cfa3-11ea-9d1f-d92ad0e64e09.png)

<br>

![wordcloud3](https://user-images.githubusercontent.com/66049273/88483614-f7121e00-cfa3-11ea-8434-de827600c552.png)

<br>

**차트 시각화**

`word <- head(sort(wordv, decreasing=T), 20)`  
상위 20개 토픽추출

`pie(word, col=rainbow(10), radius=1)`    
파이 차트 - 무지개색, 원크기

`pct <- round(word/sum(word)*100, 1)`   
백분율

`names(word)`  

키워드와 백분율 적용  
`lab <- paste(names(word), "\n", pct, "%“)`  

ex) ![image](https://user-images.githubusercontent.com/66049273/88483666-4d7f5c80-cfa4-11ea-8758-ab805602481e.png)

<br>

**연관어 분석을 위한 패키지 설치**

`install.packages("rJava")`  
`Sys.setenv(JAVA_HOME='C:/Program Files/Java/jre1.8.0_161')`  
`library(rJava)  `

`install.packages(c("KoNLP", "arules", "igraph"))`
`library(KoNLP)`

`library(arules)` # 연관규칙 라이브러리  
`library(igraph)`

<br>

**단어추출 및 단어 트랜잭션 생성**

`tran <- Map(extractNoun, fl)` # 단어 추출 - KoNLP 제공 함수

`tran <- unique(tran)` # 중복제거

`tran <- sapply(tran, unique)` # 중복제거

`tran <- sapply(tran, function(x) {Filter(function(y) + {nchar(y) <= 4 &&
nchar(y) > 1 && is.hangul(y)},x)} )`

`tran <- Filter(function(x){length(x) >= 2}, tran)` # 2자 이상 단어 필터링

`names(tran) <- paste("Tr", 1:length(tran), sep="")` # 앞쪽에 Tr 문자열 붙임

`names(tran)`

`wordtran <- as(tran, "transactions")`

`wordtab <- crossTable(wordtran)` # 교차표 작성

`wordtab`

<br>

**단어간 연관규칙 산출**

`ares <- apriori(wordtran, parameter=list(supp=0.07, conf=0.05))`

`inspect(ares)`

`rules <- labels(ares, ruleSep=" ")`

`rules <- sapply(rules, strsplit, " ", USE.NAMES=F)`

`rulemat <- do.call("rbind", rules)`

`rulemat`

ex) ![wordtran](https://user-images.githubusercontent.com/66049273/88484109-4dcd2700-cfa7-11ea-8f8f-acd58c9ba704.png)

<br>

**연관어 시각화**

연관어 시각화 - rulemat[c(34:63),] # 연관규칙 결과- {} 제거(1~33)  
`ruleg <- graph.edgelist(rulemat[c(34:63),], directed=F)`  

`plot.igraph(ruleg, vertex.label=V(ruleg)$name,vertex.label.cex=1.2, vertex.size=30,layout=layout.fruchterman.reingold.grid)`  
정점(타원) 크기 속성 : vertex.label.cex  
레이블 크기, vertext.size

ex) ![igraph](https://user-images.githubusercontent.com/66049273/88484173-c6cc7e80-cfa7-11ea-844d-3cff2427acb9.png)

정형 비정형 시리즈 끝

R 정형 비정형 시리즈 전편은 [R 정형 비정형 시리즈 1편](https://pkt369.github.io/R_Structured1)로 들어가시면 됩니다.
