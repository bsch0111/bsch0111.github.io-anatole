---
title: "python 클래스를 정의할 때 object를 붙이는 것"
date: 2020-12-13T22:15:31+09:00
Description: ""
Tags: ["python"]
Categories: ["python"]
DisableComments: false
---

# python 클래스를 정의할 때 object를 붙이는 것
참고 :https://hashcode.co.kr/questions/487/object%EB%8A%94-%EC%99%9C-%EC%83%81%EC%86%8D%EB%B0%9B%EB%8A%94-%EA%B1%B4%EA%B0%80%EC%9A%94


```python 
# python 3.x

class MyClass(object) # new-style 클래스
class MyClass # new-style 클래스

# python 2.x

class MyClass(object) : new-style 클래스
class MyClass : Old-style 클래스

```
둘 다 클래스를 선언하는 방법이여서 python 3.x 버전에서는 문제가 일어나지 않는다.  그러나 2.x 버전에서는 두 클래스 선언을 old와 new 스타일로 구분짓는다. 그래서 특별이 문제를 만들지 않기 위해선  두 버전에서 모두 new-style 클래스인 class MyClass(object) 와 같이 생성해주는게 좋다.