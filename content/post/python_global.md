---
title: " __main__ : python 모듈 호출 시 전역에 선언된 함수 수행 문제해결방법"

date: 2020-12-06T03:08:28+09:00
Description: ""
Tags: ["python","전역변수","__name__","__main__"]
Categories: ["python"]
DisableComments: false
---



# python 모듈 호출 시 전역에 선언된 함수 실행

python 모듈을 호출 했을 때 전역으로 선언되어 있는 함수, 및 변수를 수행한다.

```python
# hello1.py

print(‘hello1’)

def hello2():
	print(‘hello2’)
```

```python
# hello2,py

import hello1

hello1.hello2()

```

- python hello2.py 을 실행하면 다음과 같은 결과가 나온다. 

```python

python hello2.py                                                                                                                                      (user1)  일 12/ 6 02:38:42 2020
hello1
hello2

```

- **hello1.py 에 전역으로 작성되어 있는 print(‘hello1’) 도 같이 출력이 되었다.**



# 전역으로 선언한 함수가 import 시 수행 안되게 하는 방법

- python으로 파일을 불러올때 __main__ 이라는 이름으로 불러온다.
- 그리고 다른 파일의 import 했을때는 __main__ 이라는 이름이 아닌 파일의 명으로 불러와진다.
- 해당 파일 명은 __name__이라는 변수에 담긴다.
- 해결방안 : 다른 파일에 import 했을 때 실행시키고 싶지 않은 전역 함수 혹은 변수라면 if __name__ == ‘__main__” 구문 안에 넣어준다.

- hello1 변경
```python
# hello1.py
if __name__ == "__main__":
    print('hello1')

def hello2():
    print('hello2')



```

- 수행결과
```bash

python hello2.py                                                                                                                                      (user1)  일 12/ 6 02:51:49 2020
hello2
```
