---
title: "breakpoint 로 디버깅하기"
date: 2020-12-07T00:14:34+09:00
Description: ""
Tags: ["python","debug","debugging"]
Categories: ["python"]
DisableComments: false
---

# breakpoint 로 디버깅하기

- 참고 : https://www.askpython.com/python/built-in-methods/python-breakpoint-function
- 디버깅(debugging)은 프로그램이 정상 작동할 수 있도록 잠재적 ‘버그’를 제고하는 행위
- 파이썬에서는 pdb라는 파이썬 표준 라이브러리 모듈을 사용함 
- 예시
```python

import pdb

a = None

for i in range(10) : 
    if i == 4 :
        a = 'Hi'
        print('a is set to', a )
    elif i == 5:
        pdb.set_trace()

```
- Output
```python

> /Users/bsch0111/Desktop/git-repo/python-example/pdb-example.py(4)<module>()
-> for i in range(10) :
(Pdb) p a 
'Hi'
(Pdb) p i
5
(Pdb) exit()
```
- pdb.set_trace() : 해당 위치에서 모든 변수들의 활동을 볼 수 있음
- p [해당 위치에서 확인할 변수]
- 그러나, set_trace()는 종종 시간을 많이 소비하는 경향이 있음
- 의심이 되는 부분에서 계속 확인해봐야함
- sys 모듈을 통해 부르는 breakpoint()를 사용하면 된다.

``` python

```python

import pdb

a = None

for i in range(10) : 
    if i == 4 :
        a = 'Hi'
        print('a is set to', a )
    elif i == 5:
        breakpoint()

```

- 동일하게 pub 세션으로 넘어가는 것을 확인할 수있다
- import pdb 와 pdb.set_trace()를 안해도 된다.

## pdb 명령
참고 : http://pythonstudy.xyz/python/article/505-Python-%EB%94%94%EB%B2%84%EA%B9%85-PDB


다음은 자주 사용되는 PDB 명령들을 요약한 것이다. 명령어를 단어 전체를 사용해도 되지만, 보통 약어로 앞의 한 글자만 사용할 수 있다. 즉, next 대신 n 을 사용할 수 있다.
PDB 명령어	실행내용
help	도움말
next	다음 문장으로 이동
print	변수값 화면에 표시
list	소스코드 리스트 출력. 현재 위치 화살표로 표시됨
where	콜스택 출력
continue	계속 실행. 다음 중단점에 멈추거나 중단점 없으면 끝까지 실행
step	Step Into 하여 함수 내부로 들어감
return	현재 함수의 리턴 직전까지 실행
!변수명 = 값	변수에 값 재설정

c - continue로 다음에 설정 된 중단점으로 바로 이동
n - 다음 줄로 이동 함
r - 현재 함수가 return 될 때까지 계속 실행
l - 현재 라인을 포함하여 위 아래로 11줄의 코드를 출력함

## pdb.set_trace() 를 사용하지 않고 breakpoint()를 사용하는 이유
참고 : http://pythonstudy.xyz/python/article/505-Python-%EB%94%94%EB%B2%84%EA%B9%85-PDB

- 잘 모르겠다. 그냥 쓰자

