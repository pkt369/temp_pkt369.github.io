---

layout : posts

title : "R 정형 비정형1"

date : 2020-07-27

categories : r

---

R 정형비정형 시리즈 1입니다.

R 정형 비정형 시리즈 후편은 [R 정형 비정형 시리즈 2편](https://pkt369.github.io/R_Structured2)로 들어가시면 됩니다.

**단계1 - 토픽분석(텍스트 마이닝)**

필요한 것들 :
- 자바 64bit
- rJava : R에서 java 사용을 위한 패키지  
  - `(install.package("rJava")) `

  - `Sys.setenv(JAVA_HOME='C:\\Program Files\\Java\\jre1.8.0_161') `

  - `library(rJava)`

- `install.packages(c("KoNLP", "tm", "wordcloud"))`

사용한 데이터셋 : abstract.txt(경영학관련 저널에서 초록만 300개 추출-저널, 년도, 초록), 트위터보다 검증된 텍스트 내용

<br>

**데이터 셋 대상 자료집(documents)생성**

- Corpus() : 벡터 대상 자료집(documents)생성 함수, tm 패지키 제공

example) `result.text <- Corpus(VectorSource(data[1:100,4]))` <- 4번째 컬럼만 100개 추출하여 corpus(자료집) 생성

**분석 대상 자료집을 대상으로 NA를 공백으로 처리**

example) `result.text[is.na(result.text)] <- ""`

<br>

**세종 사전에 단어 추가**

- useSejongDic() -> 세종 사전 불러오기

`mergeUserDic(data.frame(c("비정규직", "빅데이터", "한미fta"), c("ncn")))`  
ncn - 명사지시코드

<br>

**단어 추출 사용자 함수 정의 및 단어 추출**

- 함수 실행 순서 : 단어추출 -> 문자변환 -> 공백으로 합침  
exmaple) `exNouns<- function(x) { paste(extractNoun(as.character(x)), collapse=" ")}`

-  exNouns 함수 이용 단어 추출

- 형식) sapply(적용 데이터, 적용함수) -> 요약 100개를 대상으로 단어 추출

`result_nouns <- sapply(result.text, exNouns)` # 벡터 타입으로 단어 추출

- 단어 추출 결과
`result_nouns[1]` # 1번째 백터 요소 보기

<br>

**데이터 전처리(부호, 수치, 불용어 제거)**

추출된 단어로 자료집 다시 생성  
`myCorpus <- Corpus(VectorSource(result_nouns))`

myCorpus # <<VCorpus (documents: 100, metadata (corpus/indexed): 0/0)>>

`myCorpus <- tm_map(myCorpus, removePunctuation)` # 문장부호 제거

`myCorpus <- tm_map(myCorpus, removeNumbers)` # 수치 제거

`myCorpus <- tm_map(myCorpus, tolower)` # 소문자 변경

`myCorpus <-tm_map(myCorpus, removeWords, stopwords('english'))`  
-  불용어제거 : for, very, and, of, are 등

`inspect(myCorpus[1:5])` # 데이터 전처리 결과 확인


<br>

**단어 선별(단어 길이 2개 이상)**

PlainTextDocument 함수를 이용하여 myCorpus를 일반문서로 변경

`myCorpus<-tm_map(myCorpus, PlainTextDocument)`  

`myCorpus`

TermDocumentMatrix() : 일반텍스트문서를 대상으로 단어 선별

단어길이 2개 이상인 단어만 선별 -> matrix 변경

`myTdm <- TermDocumentMatrix(myCorpus, control=list(wordLengths=c(2,Inf)))`

`myTdm # (terms: 4791, documents: 100)>> 단어 : 4791, 문서: 100`

matrix -> data.frame 변경

`mat <- as.data.frame(as.matrix(myTdm))`

`mat`

`dim(mat)` # [1] 4791 100

<br>

**단어 빈도수 구하기**

단어 빈도수 구하기 및 내림차순 정렬

`wordv <- sort(rowSums(mat), decreasing=TRUE)`

`wordv[1:5]` # 상위 5개 단어 빈도수 보기

<br>

**wordcloud 생성(디자인 전)**

`myName <- names(wordv)` # 단어 이름 생성 -> 빈도수의 이름

`wordcloud(myName, wordv)`

`myName`

ex) ![wordcloud1](https://user-images.githubusercontent.com/66049273/88483525-6b988d00-cfa3-11ea-910b-849e7aa27320.png)

<br>

R 정형 비정형 시리즈 후편은 [R 정형 비정형 시리즈 2편](https://pkt369.github.io/R_Structured2)로 들어가시면 됩니다.
