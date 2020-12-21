---
title: "Protected Getter, Setter 사용"
date: 2020-12-21T22:19:19+09:00
Description: ""
Tags: ['python']
Categories: ['python']
DisableComments: false
---
# Protected Getter, Setter 사용


```
class Car:
  def __init__(self, car_name, car_color ):
    self._car_name = car_name
    self._car_color = car_color

  @property
  def _get_car_name(self):
    return self._car_name

  def _set_car_name(self,car_name):
    if not name:
      raise Exception('invalid name')
    self._car_name = car_name

```

- protected 변수를 사용할땐 @property 데코레이터를 이용해서 getter기능을 넣을 수 있다.


1. property // setter 부분이 호출되지 않습니다.
@_set_name.setter 로 수정하는건 어떨지 여쭤봅니다

