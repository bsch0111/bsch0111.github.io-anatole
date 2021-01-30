---
title: "Requirements.txt 생성하는 방법"
date: 2021-01-31T03:48:18+09:00
Description: ""
Tags: ["python"]
Categories: ["python"]
DisableComments: false
---

파이썬에 사용되는 라이브러리를 명시하기 위해 requirements.txt가 사용된다.

global한 환경에 대한 requirements.txt 를 생성하기 위해선 아래와 같이 사용된다

```
pip freeze > requrements.txt
```
> 자신이 환경을 잘 나누어서 구축하지 않았다면 자신이 설치한 모든 라이브러리를 다 볼 수 있을 것이다.


작업하는 폴더 기준으로 의존성을 추출할때는 pigar 를 이용하면 편하다.
pip 혹은 자신의 패키지 관리자(conda 등)를 통해 pigar 를 설치한 뒤 매개변수로 폴더 경로를 입력하면
해당 폴더에 속한 python 파일들의 의존성을 검색하여 reqirements.txt 파일을 생성한다
```
pigar {의존성 파일을 생성할 경로}

```