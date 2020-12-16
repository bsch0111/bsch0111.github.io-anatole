---
title: "인덱싱과 슬라이스"
date: 2020-12-15T20:59:54+09:00
Description: ""
Tags: []
Categories: []
DisableComments: false
---

# 인덱서와 슬라이스

## 슬라이스

python 에서는 연속되는 여러개의 요소를 가진 자료형을 [시퀀스 자료형(Sequence Types)](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)이라고 한다. 그리고 이 시퀀스 자료형들은 자신의 하위요소에 접근하기 위해 슬라이스(Slice)를 문법을 사용한다.

배열 x에 사용하는 슬라이스 문법은 다음과 같다.

```python
x[start_index:stop_index:step]
```

- 수치데이터를 다루기 위해 개발된 NumPy 라이브러리는 Python 배열의 슬라이스 구문을 따르고 있으며, Numpy 배열을 기초로 만들어진 Pandas 라이브러리에서도 동일하게 슬라이스 구분을 사용할 수 있다.
- 요약하자면 배열, 문자열, Numpy 배열, Pandas의 DataFrame 에서 슬라이스 구문을 사용할 수 있다. 
- 파이썬의 슬라이스 구문이 같다는 것이지 내부 동작까지 같은건 아니다 
    - 배열의 슬라이스, DataFrame의 슬라이스는 다른 결과를 나타낼 수 있다.
    - 값 복사, 주소 복사 차이 : 배열과 DataFrame 의 슬라이스 배열의 값을 변경해본뒤 원본 배열과 DataFrame 의 값을 확인해보면 알수 있다

### 1차원 배열 DataFrame 슬라이스

- x[start:stop:step] 에서 값이 지정되지 않으면 기본으로 start = 0, stop = 배열 길이, step = 1로 지정
- step 은 다음 인덱스를 선택하는 크기

```python
import pandas as pd

x = pd.DataFrame([1,2,3,4,5,6,7,8,9,10])

print(x[:5]) # 처음부터 인덱스 4까지 (=처음부터 5개 요소)
print(x[5:]) # 인덱스 5부터 끝까지
print(x[4:7])# 인덱스 4부터 6까지
print(x[::2]) # 처음부터 요소를 하나씩 건너 뛴 배열 구성(= step인 2 배열 출력)
print(x[1::2])# 1부터 시작해서 step이 2인 배열

# step이 음수일 떄는 start와 stop의 기본값이 서로 바뀐다.
print(x[::-1]) #  모든 요소를 거꾸로 나열
print(x[9::-1]) # 인덱스 9부터 step 을 -1로 처음까지 나열
print(x[5::-2]) # 인덱스 5부터 step 을 -2로 처음까지 나열

```
- stop 이 정수로 명시된 경우 포함하지 않음 
- 기본 인덱스가 아니라 지정한 인덱스에도 잘 사용할 수 있다.

```python
import pandas as pd

x = pd.DataFrame([1,2,3,4,5,6,7,8,9,10],index=['a','b','c','d','e','f','g','h','i','j'])

print(x[:'f']) # 위의 기본 인덱스를 사용했을 때와 결과가 다르다! (생각)
print(x['f':]) 
print(x['e':'h' ]) # 위의 기본 인덱스를 사용했을 때와 결과가 다르다! (생각)
print(x[::2]) 
print(x['b'::2])


print(x[::-1]) 
print(x['j'::-1]) 
print(x['f'::-2]) 

```
- 상단의 기본인덱스를 묵시적 인덱스
- 하단의 지정한 인덱스를 명시적 인덱스


### 인덱서 loc, iloc
- 위의 표기처럼 사용하면 혼동을 줄수 있어서 인덱서를 이용해서 어떤 인덱스를 사용할것인지 표기한다.
- loc : 명시적 인덱서
- iloc : 묵시적 인덱서
- 아래를 이용해 비교해보자

```python

x = pd.DataFrame([1,2,3,4,5,6,7,8,9,10],index=['a','b','c','d','e','f','g','h','i','j'])

print('A : ' , x[1:4]) # 묵시적 인덱스
print('B : ' , x.iloc[1:4]) # 묵시적 인덱스
print('C : ' , x['b':'d']) # 명시적 인덱스
print('D : ' , x.loc['b':'d']) # 명시적 인덱스

```

### 2차원 배열 DataFrame 슬라이스
- x.loc[::,::] 앞에는 행(row), 뒤에는 열(column)을 대상으로 슬라이스를 수행
- x.iloc[::,::] 앞에는 행(row), 뒤에는 열(column)을 대상으로 슬라이스를 수행

```python
import pandas as pd

x = pd.DataFrame([[3, 5, 2, 4],
       [7, 6, 8, 8],
       [1, 6, 7, 7]], columns=['A','B','C','D'])


print(x.iloc[:2,:2]) # 두 개의 행, 두 개의 열
print(x.iloc[:2,::2]) # 두 개의 행, ['A', 'C'] 열만 출력
print(x.iloc[:2,0]) # 두 개의 행, 0 번째 열

print(x.loc[:1,:'B']) # 두 개의 행, 두 개의 열
print(x.loc[:1,::2]) # 두 개의 행, ['A', 'C'] 열만 출력
print(x.loc[:1,'A']) # 두 개의 행, 0 번째 열
```
###  2차원 배열 DataFrame 열조회
- 하나의 열 조회
    - x['열이름']
    - x.loc[:,'열이름']
- 두개 이상의 열 조회
    - x['열 배열']
    - x.loc[:,'열 배열']
```python
import pandas as pd

x = pd.DataFrame([[3, 5, 2, 4],
       [7, 6, 8, 8],
       [1, 6, 7, 7]], columns=['A','B','C','D'])

# A 열 조회
print(x['A'])
print(x.loc[:,'A'])

# B, D 열 조회
print(x[['B','D']])
print(x.loc[:,['B','D']])

```


레퍼런스

시퀀스 자료형 : https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range
pandas indexing and selecting data : https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html