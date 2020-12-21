---
title: "Private형에접근"
date: 2020-12-21T22:20:13+09:00
Description: ""
Tags: ['python']
Categories: ['python']
DisableComments: false
---
# private 형에 접근

: __로 선언되어있는 private 형 같은 경우
외부 import 되어있으면 접근할 수 없다.

그러나 내부 함수에서는 _class명__private된함수,변수명으로 접근 가능하다.

- 상속된 클래스에서도 직접 접근 안하게 하려면 private 형으로 선언할것

```python

class A(object):
  def __init__(self):
    self.__x = 15


a = A()
a._A__x # 접근가능
