---
title: "Python package란"
date: 2020-12-06T15:14:50+09:00
Description: ""
Tags: ["python","package"]
Categories: ["python"]
DisableComments: false
---

# Python Package란
- 참고 : https://docs.python.org/3/tutorial/modules.html#packages
- “dotted module names”을 이용해서 Python의 모듈을 구조화하는 방법
- 예를 들어 A.B 를 패키지로 표현한다면 B는 A의 하위 모듈임

## Python Pacakage을 만드는 방법
- ㅁ__init.py__ 을 만들면 해당 폴더를 Package라고 인식함
- ㅁ__init.py__ 은 빈 파일일수 있고, 초기화된코드를 실행하거나 ㅁ__all__ 변수를 사용할 수 있게 해줌
    * __all__은 추후에 import * 을 했을 때 사용할 수 있는 변수


## 구조화된 Package 예시

```bash
sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

### echo 모듈 ( echo.py ) 의 echofilter 함수 를 호출하는 방법
1. import sound.effects.echo
    * 다음의 사용과 비슷하다.
    * sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
2. from sound.effects import echo
    * 다음의 사용과 비슷하다.
    * echofilter(input, output, delay=0.7, atten=4)
3. from sound.effects.echo import echofilter
    * 다음의 사용과 비슷하다
    * echofilter(input, output, delay=0.7, atten=4)

### from sound.effects import *을 수행한다면?
- 이떼는 init.py 파일에 선언된 모듈이름에 대한 리스트만을 사용할 수 있다.
- 예를 들어 다음과 같이 ㅁ__init__.py에 작성되어 있을 수 있다.
```python
__all__ = [‘echo’,’surround’,’reverse’]
```
- 이 의미는 from sound.effects import *을 수행했을 때 echo, surround, reverse 세 개의 모듈을 임포트 하라는 것이다.
- 만약 ㅁ__init__.py에 아무 값도 작성되어 있지 않다면 from sound.effects import * 를 수행했을 때 어떤 모듈도 import 되지 않는다