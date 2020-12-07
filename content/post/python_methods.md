---
title: "인스턴스 메소드, 정적 메소드, 클래스 메서드"
date: 2020-12-08T02:17:16+09:00
Description: ""
Tags: ["python","methods"]
Categories: ["python"]
DisableComments: false
---

# 인스턴스 메소드, 정적 메소드, 클래스 메서드
참고 : http://pythonstudy.xyz/python/article/19-%ED%81%B4%EB%9E%98%EC%8A%A4
- 인스턴스 메소드 : 인스턴스 필드를 self 를 통해 접근할 수 있음
- 정적 메서드 : self 파라미터를 갖지 않고, 인스턴스 변수에 엑세스 할 수 없다.
    - 메서드 앞에 @staticmethod라는 Decorator를 통해 해당 메소드가 정적 메소드임을 표시 
- 클래스메서드 : cls라는 파라미터를 전달받는다. 전달받은 cls 파라미터를 통해 클래스 변수 등에 억세스 할 수 있다. (@classmethod)

```python

class Rectangle:
    count = 0  # 클래스 변수
 
    def __init__(self, width, height):
        self.width = width
        self.height = height
        Rectangle.count += 1
 
    # 인스턴스 메서드
    def calcArea(self):
        area = self.width * self.height
        return area
 
    # 정적 메서드
    @staticmethod
    def isSquare(rectWidth, rectHeight):
        return rectWidth == rectHeight   
 
    # 클래스 메서드
    @classmethod
    def printCount(cls):
        print(cls.count)   