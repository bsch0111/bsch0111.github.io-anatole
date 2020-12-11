---
title: "pandas 결측값"
date: 2020-12-12T00:35:18+09:00
Description: ""
Tags: ["pandas","missing-data"]
Categories: ["python","pandas"]
DisableComments: false
---

# pandas 결측값

참고 : 
https://m.blog.naver.com/youji4ever/221791455668

## 결측값 종류(https://purplechip.tistory.com/5)
1. None : Python 코드에서 누락된 데이터에 자주 사용되는 Python singleton 객체 (NULL이며 object 타입에 속함)
    1. Python 객체임으로 sum() 이나 min() 같은 집계함수를 이용하면 오류 발생

2. NaN : 누락된 숫자 데이터 NaN(숫자가 아님) 표준 IEEE 부동 소수점 표현에 사용하는 모든 시스템에서 인식되는 특수 부동 소수점 값을 의미,(float 타입)
    1.   사칙연산은 할수 있지만 모두 nan으로 출력
    -  데이터 바이러스 같은 형태

* pandas 에서는 non과 nan을 거의 호완성 있게 다룬다. 아래 결측 값예시에서도 데이터프레임의 None 을 NaN으로 바꾸는 것을 볼 수 있다.
* 임의의 NaN 생성할 때는 np.nan 을 사용


```python

print(1+ np.nan) -> nan 
print(1*np.nan) -> nan
 print(1-np.nan) -> nan 

```

## 결측 값 예시

``` python
df = pd.DataFrame([[0,1,2,3],
                  [None,5,None,pd.NaT],
                  [8,None,10,None],
                  [11,12,13,pd.NaT]],columns=list('ABCD'))

      A     B     C     D
0   0.0   1.0   2.0     3
1   NaN   5.0   NaN   NaT
2   8.0   NaN  10.0  None
3  11.0  12.0  13.0   NaT

```

결측값을 확인할 수 있는 방법

### Pandas 누락된 값 처리하기
* isnall() : 누락 값을 가리키는 부울 마스크 생성
* notnull() : isnull()의 역
* dropna() : 데이터에 필터를 적용한 버전
* fillna() : 누락값을 채우거나 전가된 데이터 사본을 변환


df.isnull() : 결측값 확인하기 (True, False 에 대한 data frame 으로 반환)
```python
print(df008770.isna())


    주요재무정보  2019/09\n(IFRS연결)  ...  2021/03(E)\n(IFRS연결)  2021/06(E)\n(IFRS연결)
0    False              False  ...                 False                 False
1    False              False  ...                 False                 False
2    False              False  ...                  True                  True
3    False              False  ...                 False                 False
4    False              False  ...                 False                 False
5    False              False  ...                 False                 False
6    False              False  ...                  True                  True
7    False              False  ...                  True                  True

```


df.isnull().sum() : column 별로 결측값 확인
df.isnull().sum(1) : row 별로 결측값 확인

df = df.fillna(0) # 결측치를 0으로 변경
df = df.dropna() # 결측치와 관련된 행 제거

결측치 처리 예시

``` python

# 널 값 탐지

data = pd.Series([1,2,3,4,np.nan,20301,np.nan])
data.isnull()

# 부울 마스크 사용해서 인덱스로 활용

0    False
1    False
2    False
3    False
4     True
5    False
6     True
dtype: bool

# 널 개수 세기
data.isnull().sum()

2

# 널 있는지 확인하기
data.isnull().any()

True

#널 데이터 value 확인
data[data.isnull()]

4   NaN
6   NaN
dtype: float64

#널 데이터가 아닌 value 확인

data[data.notnull()]

0        1.0
1        2.0
2        3.0
3        4.0
5    20301.0
dtype: float64

```

```python

# 널값 제거하기
# 마스킹을 시용하는 방법 : data[isnull()] = _____
# 1. dropna()       2. fillna()

df = pd.DataFrame(data = [[1,np.nan, 2],
                  [2, 3, 5],
                  [np.nan, 4, 6]])
df

		 0    1  2
0  1.0  NaN  2
1  2.0  3.0  5
2  NaN  4.0  6

# DataFrame은 단일 값만 삭제할 수 없음
# 행 혹은 열을 전부 삭제

# 기본 dropna는 널 값이 있는 행을 모두 삭제
# df.dropna(axis='rows') 가능
# df.dropna(axis = 0)
df.dropna()

		0	  1	2
1	2.0	3.0	5

# 열을 기준으로 삭제
# df.dropna(axis='columns') 가능
df.dropna(axis = 1)

   2
0  2
1  5
2  6

# 모두 Na로 채워져 있는 행만 삭제 하고 싶을때
df[3] = np.nan
df

      0    1  2  3
0  1.0  NaN  2 NaN
1  2.0  3.0  5 NaN
2  NaN  4.0  6 NaN

 # NaN를 모두 포함하는 열만 삭제
df.dropna(axis='columns',how='all')

     0    1  2
0  1.0  NaN  2
1  2.0  3.0  5
2  NaN  4.0  6

# NaN이 아닌 값이 3개 이상있는 행만 남기고 싶을 떄
df.dropna(axis='rows', thresh=3)

     0    1  2   3
1  2.0  3.0  5 NaN

# 널 값 채우기
#df[df.isnull()]= __ 이렇게 채울수도 있지만

# fillna()를 사용하는게 제공되는게 많음

print(df.fillna(0))

     0    1  2    3
0  1.0  0.0  2  0.0
1  2.0  3.0  5  0.0
2  0.0  4.0  6  0.0

#forward-fill(이전 값으로 채우기)
df.fillna(method='ffill', axis = 'columns')
#제일 앞에 있는 컬럼은 채우지 못함

     0    1    2    3
0  1.0  1.0  2.0  2.0
1  2.0  3.0  5.0  5.0
2  NaN  4.0  6.0  6.0

#backwod-rill(다음에 오는 값으로 채우기)
print(df.fillna(method='bfill',axis = 'columns'))

     0    1    2   3
0  1.0  2.0  2.0 NaN
1  2.0  3.0  5.0 NaN
2  4.0  4.0  6.0 NaN

```




## isnull vs isna 

isnull vs isna : 둘이 같은 기능을 수행함
https://qastack.kr/datascience/37878/difference-between-isna-and-isnull-in-pandas


## Na, Null, None, NaN

기본 정의
- Na: 잘못된 값
- Null : 아직 정해지지 않은 값

null
- 정해지지 않은 값
- 아무것도 표현하지 않은 상태
- 대부분 고의적으로 null 값을 지정

None, NaN
- String은 None 으로 저장하면 None 으로 저장됨
- int를 None으로 저장하면 NaN으로 저장됨

* pandas에서는 NaN 으로 Na, Null을 모두 ** 아직 정해지지 않은 값**으로 표시


