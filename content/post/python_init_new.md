---
title: "python 클래스 인스턴스를 생성할 때 함수(init,new) 호출 순서 "
date: 2020-12-08T02:14:02+09:00
Description: ""
Tags: ["python","init","new"]
Categories: ["python"]
DisableComments: false
---
# python 클래스 인스턴스를 생성할 때 함수 호출 순서 
참고 : https://wikidocs.net/16071
1. o __new__ : 클래스 자체를 받으며 할당하게되고
2. o __init__ : 객체의 내부에서 사용할 속성을 초기화

