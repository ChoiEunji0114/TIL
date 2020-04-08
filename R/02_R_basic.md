# Basic R Tutorial
> 참고 : R통계분석 강의자료 (2019-1) 

### 기본 명령어 ✍️

- ```<-```, ```=``` : 변수에 값 지정
- ```rm()``` : 변수 삭제
- ```ls()``` : 현재 사용 중인 모든 변수 보기
- ```rm(list=ls())``` : 현재 사용 중인 모든 변수 삭제
- ```getwd()``` : 현재 작업하는 working directory 를 보여 줌
- ```setwd()``` : working directory 를 바꿈
- ```cat("")``` : 특정 문자열을 화면에 보여줌
- ```head()``` : 데이터의 앞 부분을 보여 줌. default 는 6.   
```head(iris, n=10)``` 와 같이 보고 싶은 데이터 수를 지정할 수도 있음
- ```tail()``` : 데이터의 끝 부분을 보여 줌
- ```summary()``` : mean, max, min 값 등 데이터의 요약본을 보여 줌

<br/>

## Vector
동일한 형태의 자료를 **1차원** 형태로 여러 개 모아서 취급하는 데이터 형태이다.

### 📌 벡터형 자료의 생성

```r
> v1 = c(1,2,3,4,5)
> v1
[1] 1 2 3 4 5
> v2 = -5:5
> v2
 [1] -5 -4 -3 -2 -1  0  1  2  3  4  5
> v3 = seq(from=1, to=5, by=0.5)
> v3
[1] 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0
> v4 = rnorm(20)
> v4
 [1]  1.0958286  0.4925178 -1.4461587 -1.9449052  0.1659416  0.6598200
 [7] -0.5485212  0.9387832  1.1153385  0.2525385  0.1993640 -0.8533704
[13] -0.3376990 -2.4247526 -1.9302436  1.5409397  1.3792199 -0.8041084
[19] -2.5204656 -0.5280681
```

- ```c()``` : 벡터형 자료 생성
- ```N1 : N2``` : N1 부터 N2까지 벡터 생성
- ```seq(from=n1, to=n2, by=n3)``` : n1부터 n2까지 n3의 간격을 가진 벡터 생성
- ```rnorm(n)``` : 0~1 사이의 난수 n개 생성

<br/>

### 📌 벡터형 자료의 기본 연산

```r
> mean(v1)
[1] 3
> order(v1)
[1] 1 2 3 4 5
> rev(v1)
[1] 5 4 3 2 1
> range(v1)
[1] 1 5
> sd(v2)
[1] 3.316625
> sort(v4)
 [1] -2.5204656 -2.4247526 -1.9449052 -1.9302436 -1.4461587 -0.8533704
 [7] -0.8041084 -0.5485212 -0.5280681 -0.3376990  0.1659416  0.1993640
[13]  0.2525385  0.4925178  0.6598200  0.9387832  1.0958286  1.1153385
[19]  1.3792199  1.5409397
> sort(v4, decreasing = TRUE)
 [1]  1.5409397  1.3792199  1.1153385  1.0958286  0.9387832  0.6598200
 [7]  0.4925178  0.2525385  0.1993640  0.1659416 -0.3376990 -0.5280681
[13] -0.5485212 -0.8041084 -0.8533704 -1.4461587 -1.9302436 -1.9449052
[19] -2.4247526 -2.5204656
> length(v4)
[1] 20
```

- ```mean(x)``` : x의 평균
- ```order(x)``` : x를 오름차순으로 정렬 (인덱스를 표시)
- ```rev(x)``` : x를 역순으로 정렬
- ```range(x)``` : x의 범위를 구함
- ```sd(x)``` : x의 표준편차
- ```sort(x)``` : 오름차순 정렬
- ```sort(x, decreasing = TRUE)``` : 내림차수 정렬
- ```length(x)``` : x의 길이

<br/>

### 📌 벡터형 자료 조작

```r
> x = c(1,4,6,8,9)
> x
[1] 1 4 6 8 9
> x[2]
[1] 4
> x[-2]
[1] 1 6 8 9
> x[3] = 4
> x
[1] 1 4 4 8 9
> x[2>x & x<5]
[1] 1
```
- ```x[-2]``` : x의 2번째 원소를 제외함
- ```x[2<x & x<5]``` : 조건에 맞는 원소를 추출함

```r
> x = c(1,4,6,8,9)
> x
[1] 1 4 6 8 9
> y = replace(x, c(2,4), c(32,24))
> y
[1]  1 32  6 24  9
> w = append(x,y)
> w
 [1]  1  4  6  8  9  1 32  6 24  9
> z = append(x, y, after=2)
> z
 [1]  1  4  1 32  6 24  9  6  8  9
> c(1,2) + c(4,5)
[1] 5 7
> c(1,2,3) + 1
[1] 2 3 4
```

- ```replace(x, c(2,4), c(32,24)``` : x의 2번째, 4번째 원소를 32, 24로 바꾼다 
- ```append(x,y) ``` : x,y 벡터를 합친다

<br/>

### 📌 집합 연산

```r
> x = c(1,2,3)
> y = c(4,5,6)
> x==y # 순서에 따른 집합 비교
[1] FALSE FALSE FALSE
> union(x,y)
[1] 1 2 3 4 5 6
> intersect(x,y)
numeric(0)
> setdiff(x,y)
[1] 1 2 3
> setequal(x,y) # 같은 집합인지 비교
[1] FALSE
> is.element(3,x)
[1] TRUE
```
- ```union(x,y)``` : x,y 의 합집합
- ```intersect(x,y)``` : x,y의 교집합
- ```setdiff(x,y)``` : x-y (차집합)
- ```setequal(x,y)``` : x,y 가 같은 집합인지 비교
- ```is.element(3,x)``` : 3이 x의 원소인지 판별


```r
> x = rep(c("a", "b", "c"), times=4)
> x
 [1] "a" "b" "c" "a" "b" "c" "a" "b" "c" "a" "b" "c"
> unique(x)
[1] "a" "b" "c"
> match(x,c("a"))
 [1]  1 NA NA  1 NA NA  1 NA NA  1 NA NA
> 
> y = c("d", "e", "f")
> y
[1] "d" "e" "f"
> z = paste(x[1], y[3])
> z
[1] "a f"
```

```r
> x = runif(5)
> x
[1] 0.5358869 0.8370841 0.6883361 0.7370992 0.7321462
> (0.4<=x) & (x<=0.7)
[1]  TRUE FALSE  TRUE FALSE FALSE
> any(x>0.8)
[1] TRUE
> all(x<0.7)
[1] FALSE
> is.vector(x)
[1] TRUE
```

<br/>

## Matrix

**동일한 형태**의 자료를 **2차원** 형태로 여러 개 모아 취급하는 데이터 형태   
벡터 데이터를 생성한 후 합쳐서 생성한다.

### 📌 행렬 데이터 생성

```r
> row1 = c(1,2,3)
> row1
[1] 1 2 3
> row2 = c(4,5,6)
> row2
[1] 4 5 6
> row3 = c(7,8,9)
> row3
[1] 7 8 9
> mat1 = rbind(row1, row2, row3)
> mat1
     [,1] [,2] [,3]
row1    1    2    3
row2    4    5    6
row3    7    8    9
> mat2 = cbind(row1, row2, row3)
> mat2
     row1 row2 row3
[1,]    1    4    7
[2,]    2    5    8
[3,]    3    6    9
```
- ```rbind()``` : row 를 기준으로 벡터를 묶어 행렬 생성
- ```cbind()``` : column 을 기준으로 벡터를 묶어 행렬 생성

```r
> chars = c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j")
> 
> chars
 [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j"
> mat1 = matrix(chars) # ncol default 값은 1이다.
> mat1 
      [,1]
 [1,] "a" 
 [2,] "b" 
 [3,] "c" 
 [4,] "d" 
 [5,] "e" 
 [6,] "f" 
 [7,] "g" 
 [8,] "h" 
 [9,] "i" 
[10,] "j" 
> 
> mat2 = matrix(chars, ncol=5)
> mat2
     [,1] [,2] [,3] [,4] [,5]
[1,] "a"  "c"  "e"  "g"  "i" 
[2,] "b"  "d"  "f"  "h"  "j" 
> 
> mat3 = matrix(chars, nrow=5)
> mat3
     [,1] [,2]
[1,] "a"  "f" 
[2,] "b"  "g" 
[3,] "c"  "h" 
[4,] "d"  "i" 
[5,] "e"  "j" 
```

<br/>

### 📌 행렬 데이터 조작 & 추출

```r
> mat3 = matrix(1:8, nrow=2)
> mat3
     [,1] [,2] [,3] [,4]
[1,]    1    3    5    7
[2,]    2    4    6    8
> mat3*3
     [,1] [,2] [,3] [,4]
[1,]    3    9   15   21
[2,]    6   12   18   24
> mat3*c(10,20) # 첫 번째 행에는 10곱하기, 두 번째 행에는 20곱하기
     [,1] [,2] [,3] [,4]
[1,]   10   30   50   70
[2,]   40   80  120  160
>
```
```r
> x = matrix(1:12, nrow=3, dimnames=list(c("R1","R2","R3"), c("C1", "C2", "C3", "C4")))
> x
   C1 C2 C3 C4
R1  1  4  7 10
R2  2  5  8 11
R3  3  6  9 12
> x[7] 
[1] 7
> x[1,] # 1번째 행 추출
C1 C2 C3 C4 
 1  4  7 10 
> x[,2:4]
   C2 C3 C4
R1  4  7 10
R2  5  8 11
R3  6  9 12
> x[,2] # 2번째 열 추출
R1 R2 R3 
 4  5  6 
> x[,-2] # 2번째 열 제외하고 추출
   C1 C3 C4
R1  1  7 10
R2  2  8 11
R3  3  9 12
```

```r
> mat1 = matrix(1:9, ncol=3, dimnames=list(c("row1", "row2", "row3"), c("col1", "col2", "col3")))
> mat1
     col1 col2 col3
row1    1    4    7
row2    2    5    8
row3    3    6    9
> apply(mat1, 1, max) # 각 row의 max값 추출
row1 row2 row3 
   7    8    9 
> apply(mat1, 2, max) # 각 column의 max값 추출
col1 col2 col3 
   3    6    9 
> mean(mat1[2,]) # 2번째 row의 mean값
[1] 5
> apply(mat1, 1, sum) # mat1의 각 row의 sum
row1 row2 row3 
  12   15   18 
> apply(mat1, 1, mean) # mat1의 각 row의 mean
row1 row2 row3 
   4    5    6 
```

<br/>

## DataFrame

2차원 형태로 각 컬럼별로 다른 형태의 데이터를 가짐   
배열 데이터를 모아 구성함

```r
> no = c(1,2,3,4)
> name = c("Apple", "Banana", "Peach", "Berry")
> prices = c(500,200,200,50)
> qty = c(5,2,7,9)
> 
> fruit = data.frame(No=no, Name=name, Prices=prices, QTY=qty)
> fruit
  No   Name Prices QTY
1  1  Apple    500   5
2  2 Banana    200   2
3  3  Peach    200   7
4  4  Berry     50   9
> 
> fruit[1,]
  No  Name Prices QTY
1  1 Apple    500   5
> 
> fruit[,2:3]
    Name Prices
1  Apple    500
2 Banana    200
3  Peach    200
4  Berry     50
> fruit[,-2]
  No Prices QTY
1  1    500   5
2  2    200   2
3  3    200   7
4  4     50   9
```

```r
> name=c("kang", "kang2", "kwon", "kwon2")
> eng = c(90, 80, 60, 70)
> mat = c(50, 60, 100, 20)
> score = data.frame(Name=name, Eng=eng, Mat=mat)
> score
   Name Eng Mat
1  kang  90  50
2 kang2  80  60
3  kwon  60 100
4 kwon2  70  20
> 
> score$avg=(score$Eng+score$Mat)/2 # 파생변수 생성
> score
   Name Eng Mat avg
1  kang  90  50  70
2 kang2  80  60  70
3  kwon  60 100  80
4 kwon2  70  20  45
```
<br/>

## List

키, 값의 형태로 데이터가 구성됨


```r
> # member list 생성
> member=list(name="Choi", address="Seoul", tel="01011112222", gender="F")
> member
$name
[1] "Choi"

$address
[1] "Seoul"

$tel
[1] "01011112222"

$gender
[1] "F"

> 
> member$name # 조회
[1] "Choi"
> member[1:2] # 조회
$name
[1] "Choi"

$address
[1] "Seoul"

> member$job="student" # 추가
> member
$name
[1] "Choi"

$address
[1] "Seoul"

$tel
[1] "01011112222"

$gender
[1] "F"

$job
[1] "student"
```

<br/>




