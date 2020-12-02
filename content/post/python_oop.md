---
title: "Python_oop"
date: 2020-12-03T00:43:40+09:00
Description: ""
Tags: ["python","oop"]
Categories: ["프로그래밍"]
DisableComments: false
---
# PYTHON과 객체지향프로그래밍

## 객체지향 프로그램?

위키백과
- 여러 개의 독립된 단위, 즉 "객체"들의 모임으로 파악하고자 하는 것이다.
- 객체 지향 프로그래밍은 프로그램을 유연하고 변경이 용이하게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용된다

프로그램을 유연하고 변경이 용이하도록 만들기 위함
대규모 프로젝트 및 코딩의 시간을 줄여줌

일반적으로 프로그램을 만들때 항상 염두에 둬야할 아주 중요한 포인트 2가지가 있습니다.
- 같은 코드를 반복하지 않는다.
- 코드는 항상 바뀔 수 있다는 것을 기억한다.

## 예제의 코드를 클래스 형태로 변형해보자
참고

http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-1-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8Doop%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-%EC%99%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%EA%B0%80/

```python
monster_1_name = '고블린'
monster_1_health = 90
monster_1_damage = 30
monster_1_inventory = [
    {'gold': 50},
    {'weapon': '창'}
]
```
### 클래스로의 변경
```python
class monster :
  def __init__(self,name,health,damage,inventory) :
    self._name = name
    self._health = health
    self._damage = damage
    self._inventory = [{'gold': inventory[0],
                        'weapon' : inventory[1]}]
  def __repr__(self) :
    return self._name
    pass
```
출력
```python
monster1 = monster('아이언맨',100,50,[5000,'자비스'])

monster1._inventory
-> [{'gold': 5000, 'weapon': '자비스'}]

monster1
-> 아이언맨
```

#### __repr__ 의 역활

https://shoark7.github.io/programming/python/difference-between-__repr__-vs-__str__ 정리 필요

나는 어느정도 까지 공부해야 할까
Python이라는 것에 대해서 어디까지 공부 해야할까 공부하고 싶은 분야마다 학회가 열릴 정도로 깊은 학문들인데 다 하는 것은 말도 안된다고 생각한다. 어디까지 아는게 할 수 있는 정도 일까.

하나하나해보다가 실력이 생기면 어느 정도의 레벨 업이 되는 것일까
