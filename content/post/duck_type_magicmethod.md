---
title: "Duck_typer과 매직 메소드와 private형 변수 접근"
date: 2020-12-21T22:18:09+09:00
Description: ""
Tags: ['python']
Categories: ['python']
DisableComments: false
---


# 클래스 생성시 필요한 부분

## Duck Typing
- 객체의 상속을 이용하지 않고, 해당 기능을 하는 method가 있는지만을 파악하는것
- 만약 어떤 새가 오리처럼 걷고, 헤엄치고, 꽥꽥거리는 소리를 낸다면 나는 그 새를 오리라고 부를 것이다.
```python

class Parrot:
    def fly(self):      # 첫번째 fly 함수
        print("Parrot flying")

class Airplane:
    def fly(self):      # 두번째 fly 함수
        print("Airplane flying")

```

## 매직 매소드
- 특정한 문법적인 기능을 제공하거나, 특정 일을 수행한다.
- __init__ 
    - 생성자 역활을 하는 메소드
- __str__
    - print 를 호출했을 때 나올 출력값 정의

```python

class Student(object):
  def __str__(self):
    return “나는 학생입니다.”

```

- __repr__
    - 인터프린터가 이해하고 있는 상태를 반환해준다
    - 문자열 같은게 잘 안될때 사용하면 좋을 듯
    - object를 반환
```python

hello = 'hello, world\n'
hello.__str__()
->  hello, world\n

repr(hello)
'hello, world\\n'
```


새롭게 알게된 것
: __로 선언되어있는 private 형 같은 경우
외부 import 되어있으면 접근할 수 없다.

그러나 내부 함수에서는 _class명__private된함수,변수명으로 접근 가능하다.

```python

class A(object):
  def __init__(self):
    self.__x = 15


a = A()
a._A__x # 접근가능

```