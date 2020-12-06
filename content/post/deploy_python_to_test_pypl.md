---
title: "test_pypl에 패키지 배포하기"
date: 2020-12-06T15:12:00+09:00
Description: ""
Tags: ["python","deploy","test pypl"]
Categories: ["python"]
DisableComments: false
---

2020/12/05 5. test pypl 에 패키지 배포


# test pypl 에 패키지 배포 과정

- PyPI : Python Package Index (PyPI)
- 1 우선 package 를 만들고, 배포가 가능하도록 README.md, LICENSE, setup.py 파일을 구성 
- 2 그 다음 test pypl 사이트에 가입을 하고
- 3 파이썬 코드를 컴퓨터가 읽을 수 있도록 변경 (빌드하기)
- 4 test pypl 에 배포

## Python Package
- Python Package란 포스팅 참고
- package 할 다이렉트에 __init__.py를 생성해야한다는 것은 기억 !

## 테스트 서버인 test PyPI 에 배포해보기
- 1. 배포하기 위해서는 3개의 파일이 추가적으로 필요함
    - 1 README.md
        * 해당 패키지를 검색했을 떄 나오는 설명
    - 2 LICENSE
        * 라이선스 정보
    - 3 setup.py
        * 참고 : https://qastack.kr/programming/1471994/what-is-setup-py
        * 저자 정보, 설치해야할 것들이 담겨 있는 파일
        * 얘룰 들어 foo 라는 패키지를 version 1.0이라고 지정하고 저자를 man foo로 지정하고 싶다면 다음과 같이 구성하면된다

``` python

from setuptools import setup

setup(
   name='foo',
   version='1.0',
   description='A useful module',
   author='Man Foo',
   author_email='foomail@foo.com',
   packages=['foo'],  #same as name
   install_requires=['bar', 'greek'], #external packages as dependencies
)

```
- 만들어진 트리 구조

```bash
./
├── LICENSE
├── README.md
├── hello_back
│   ├── __init__.py
│   └── hello1.py
└── setup.py

1 directory, 5 files


```

2. test pypl 사이트에 가입 후 이메일 검증 실행
3. 빌드하기(컴퓨터가 이해할 수 있는 언어로 바꾸기),
- setup 설정을 setuptools로 했으므로 pip3 list를 통해 setuptools가 설치되어 있는지 확인
```bash

pip3 list                                                                                                                                                (user1)  일 12/ 6 14:46:41 2020
Package    Version
---------- -------
pip        19.2.3
setuptools 41.2.0
six        1.15.0
wheel      0.33.1

```

-  빌드하는 방법은 여러가지가 이지만 공식적으로는 wheel을 사용하는 방법이 권장된다고 한다 ( https://rampart81.github.io/post/python_package_publish/ )
```bash
python setup.py bdist_wheel
```

- 배포하기
    - 배포는 twine 이라는 패키지를 통해 수행
    - twine 설치
```bash
	python -m pip install --user --upgrade twine
```
    - 업로드 해야하는건 dist 폴더의 내용이다. testpypi에 업로드 해보도록 하겠다
```bash
	python -m twine upload --repository testpypi dist/*
```

올라간거 확인할 수 있다..
아직 markdown을 이용해서 이미지 업로드하는게 번거롭다.. 어떻게 쉬운방법이 없을까


