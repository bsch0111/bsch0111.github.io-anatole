---
title: "가정 설정문(Assert) "
date: 2020-12-17T01:56:58+09:00
Description: ""
Tags: ['python']
Categories: ['python']
DisableComments: false
---

# 가정 설정문(assert)

- assert는 뒤의 조건이 True 가 아니면 AssertError 를 발생
- assert condition ‘message’로 구성
- message는 AssertionError 와 같이 출력

```python

a = 3
assert a == 3 , ‘a는 3이 아니다’
assert a == 5 , ‘a는 5가 아니다’


      2 a = 3
      3 assert a == 3 , 'a는 3이 아니다'
----> 4 assert a == 5 , 'a는 5가 아니다'

AssertionError: a는 5가 아니다
  
```