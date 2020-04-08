# R 데이터 처리 & 가공 

- **데이터 전처리** : 분석에 적합하게 데이터를 가공하는 작업   
일부 추출, 종류별로 나누기, 여러 데이터 합치기 등의 작업 수행
  
🗂 **dplyr** : 데이터 전 처리 작업에 많이 사용되는 패키지

- ```filter()``` : 행 추출
- ```select()``` : 열(변수) 추출
- ```arrange()``` : 정렬
- ```mutate()``` : 변수 추가
- ```summarize()``` : 통계치 산술
- ```group_by``` : 집단별로 나누기
- ```left_join()``` : 데이터 합치기 (열)
- ```bind_rows()``` : 데이터 합치기 (행)

<br/>

## 데이터 가공

### 📌 filter : 추출

```r
> ### 샘플 데이터 exam 불러오기
>
> exam=read.csv("exam.csv")
> exam
   id class math english science
1   1     1   50      98      50
2   2     1   60      97      60
3   3     1   45      86      78
4   4     1   30      98      58
5   5     2   25      80      65
6   6     2   50      89      98
7   7     2   80      90      45
8   8     2   90      78      25
9   9     3   20      98      15
10 10     3   50      98      45
11 11     3   65      65      65
12 12     3   45      85      32
13 13     4   46      98      65
14 14     4   48      87      12
15 15     4   75      56      78
16 16     4   58      98      65
17 17     5   65      68      98
18 18     5   80      78      90
19 19     5   89      68      87
20 20     5   78      83      58
```

```r
> # 추출
> exam %>% filter(class==1) # 1반 학생
  id class math english science
1  1     1   50      98      50
2  2     1   60      97      60
3  3     1   45      86      78
4  4     1   30      98      58
> exam %>% filter(math>50) # 수학 50점 넘는 학생
   id class math english science
1   2     1   60      97      60
2   7     2   80      90      45
3   8     2   90      78      25
4  11     3   65      65      65
5  15     4   75      56      78
6  16     4   58      98      65
7  17     5   65      68      98
8  18     5   80      78      90
9  19     5   89      68      87
10 20     5   78      83      58
>
> exam %>% filter(class==1 & math>50) # 수학 50점 넘는 1반학생
  id class math english science
1  2     1   60      97      60
>
> exam %>% filter(class%in%c(1,3,5)) # 1,3,5반 학생
   id class math english science
1   1     1   50      98      50
2   2     1   60      97      60
3   3     1   45      86      78
4   4     1   30      98      58
5   9     3   20      98      15
6  10     3   50      98      45
7  11     3   65      65      65
8  12     3   45      85      32
9  17     5   65      68      98
10 18     5   80      78      90
11 19     5   89      68      87
12 20     5   78      83      58
```

<br/>

### 📌 select : 변수 추출

```r
> # 변수 추출
> exam %>% select(class, english)
   class english
1      1      98
2      1      97
3      1      86
4      1      98
5      2      80
6      2      89
7      2      90
8      2      78
9      3      98
10     3      98
11     3      65
12     3      85
13     4      98
14     4      87
15     4      56
16     4      98
17     5      68
18     5      78
19     5      68
20     5      83
```
```r
> # 1반 학생들의 영어 점수
> exam %>% filter(class==1) %>% select(english)
  english
1      98
2      97
3      86
4      98
```

<br/>

### 📌 arrange : 정렬

```r
> exam %>% arrange(math) # 수학 점수 오름차순으로 정렬
   id class math english science
1   9     3   20      98      15
2   5     2   25      80      65
3   4     1   30      98      58
4   3     1   45      86      78
5  12     3   45      85      32
6  13     4   46      98      65
7  14     4   48      87      12
8   1     1   50      98      50
9   6     2   50      89      98
10 10     3   50      98      45
11 16     4   58      98      65
12  2     1   60      97      60
13 11     3   65      65      65
14 17     5   65      68      98
15 15     4   75      56      78
16 20     5   78      83      58
17  7     2   80      90      45
18 18     5   80      78      90
19 19     5   89      68      87
20  8     2   90      78      25
>
> exam %>% arrange(desc(math)) # 수학점수 내림차순 정렬
   id class math english science
1   8     2   90      78      25
2  19     5   89      68      87
3   7     2   80      90      45
4  18     5   80      78      90
5  20     5   78      83      58
6  15     4   75      56      78
7  11     3   65      65      65
8  17     5   65      68      98
9   2     1   60      97      60
10 16     4   58      98      65
11  1     1   50      98      50
12  6     2   50      89      98
13 10     3   50      98      45
14 14     4   48      87      12
15 13     4   46      98      65
16  3     1   45      86      78
17 12     3   45      85      32
18  4     1   30      98      58
19  5     2   25      80      65
20  9     3   20      98      15
> exam %>% arrange(class, math) # 반별로 수학점수 오름차순 정렬
   id class math english science
1   4     1   30      98      58
2   3     1   45      86      78
3   1     1   50      98      50
4   2     1   60      97      60
5   5     2   25      80      65
6   6     2   50      89      98
7   7     2   80      90      45
8   8     2   90      78      25
9   9     3   20      98      15
10 12     3   45      85      32
11 10     3   50      98      45
12 11     3   65      65      65
13 13     4   46      98      65
14 14     4   48      87      12
15 16     4   58      98      65
16 15     4   75      56      78
17 17     5   65      68      98
18 20     5   78      83      58
19 18     5   80      78      90
20 19     5   89      68      87
```

<br/>

### 📌 mutate : 파생 변수 추가

```r
> exam %>% mutate(total=math+english+science, 
mean=(math+english+science)/3, 
test=ifelse(science>=60, "pass", "fail"))
   id class math english science total     mean test
1   1     1   50      98      50   198 66.00000 fail
2   2     1   60      97      60   217 72.33333 pass
3   3     1   45      86      78   209 69.66667 pass
4   4     1   30      98      58   186 62.00000 fail
5   5     2   25      80      65   170 56.66667 pass
6   6     2   50      89      98   237 79.00000 pass
7   7     2   80      90      45   215 71.66667 fail
8   8     2   90      78      25   193 64.33333 fail
9   9     3   20      98      15   133 44.33333 fail
10 10     3   50      98      45   193 64.33333 fail
11 11     3   65      65      65   195 65.00000 pass
12 12     3   45      85      32   162 54.00000 fail
13 13     4   46      98      65   209 69.66667 pass
14 14     4   48      87      12   147 49.00000 fail
15 15     4   75      56      78   209 69.66667 pass
16 16     4   58      98      65   221 73.66667 pass
17 17     5   65      68      98   231 77.00000 pass
18 18     5   80      78      90   248 82.66667 pass
19 19     5   89      68      87   244 81.33333 pass
20 20     5   78      83      58   219 73.00000 fail
```

<br/>

### 📌 group_by(), summarise() : 집단별 요약

```r
> exam %>% 
+ group_by(class) %>%
+ summarise(mean_math=mean(math),)
# A tibble: 5 x 2
  class mean_math
  <int>     <dbl>
1     1      46.2
2     2      61.2
3     3      45  
4     4      56.8
5     5      78  
> exam %>% 
+ group_by(class) %>%
+ summarise(mean_math=mean(math), sum_math=sum(math), median_math=median(math), n=n())
# A tibble: 5 x 5
  class mean_math sum_math median_math     n
  <int>     <dbl>    <int>       <dbl> <int>
1     1      46.2      185        47.5     4
2     2      61.2      245        65       4
3     3      45        180        47.5     4
4     4      56.8      227        53       4
5     5      78        312        79       4
```

<br/>

### 📌 left_join() : 데이터 가로로 합치기 

```r
> test1 = data.frame(id=c(1,2,3,4,5), midterm=c(10,20,30,40,50))
> test2 = data.frame(id=c(1,2,3,4,5), final=c(50,60,70,80,90))
> 
> total = left_join(test1,test2,by="id")
> total
  id midterm final
1  1      10    50
2  2      20    60
3  3      30    70
4  4      40    80
5  5      50    90
```

```r
> name=data.frame(class=c(1,2,3,4,5), teacher=c("Kim", "Lee", "Park", "Choi", "Jung"))
> name
  class teacher
1     1     Kim
2     2     Lee
3     3    Park
4     4    Choi
5     5    Jung
> 
> exam_new = left_join(exam, name, by="class")
> exam_new
   id class math english science teacher
1   1     1   50      98      50     Kim
2   2     1   60      97      60     Kim
3   3     1   45      86      78     Kim
4   4     1   30      98      58     Kim
5   5     2   25      80      65     Lee
6   6     2   50      89      98     Lee
7   7     2   80      90      45     Lee
8   8     2   90      78      25     Lee
9   9     3   20      98      15    Park
10 10     3   50      98      45    Park
11 11     3   65      65      65    Park
12 12     3   45      85      32    Park
13 13     4   46      98      65    Choi
14 14     4   48      87      12    Choi
15 15     4   75      56      78    Choi
16 16     4   58      98      65    Choi
17 17     5   65      68      98    Jung
18 18     5   80      78      90    Jung
19 19     5   89      68      87    Jung
20 20     5   78      83      58    Jung
```

<br/>

### 📌 bind_rows() : 데이터 세로로 합치기

```r
> group_a = data.frame(id=c(1,2,3,4,5), test=c(60,70,80,90,100))
> group_b = data.frame(id=c(1,2,3,4,5), test=c(70,83,65,95,80))
> group_all = bind_rows(group_a, group_b)
> group_all
   id test
1   1   60
2   2   70
3   3   80
4   4   90
5   5  100
6   1   70
7   2   83
8   3   65
9   4   95
10  5   80
```
