---
title: "Python class 변수 , 인스턴스 변수"
date: 2020-12-08T02:15:47+09:00
Description: ""
Tags: ['python','class variable', 'instance variable']
Categories: ['python']
DisableComments: false
---
# class 변수 , 인스턴스 변수
참고 : http://pythonstudy.xyz/python/article/19-%ED%81%B4%EB%9E%98%EC%8A%A4
```python

class Rectangle:
    count = 0  # 클래스 변수
 
    # 초기자(initializer)
    def __init__(self, width, height):
        # self.* : 인스턴스변수
        self.width = width
        self.height = height
        Rectangle.count += 1
 
    # 메서드
    def calcArea(self):
        area = self.width * self.height
        return area
```

- 클래스 변수 : 클래스 하나가 공통으로 사용하는 변수
- 인스턴스 변수 : 각 인스턴스가 개별적으로 생성해서 사용하는 변수
