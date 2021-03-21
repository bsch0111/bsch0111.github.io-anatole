---
title: "FLASK_정리_1"
date: 2021-03-22T00:55:20+09:00
draft: true
---

## FLASK 기본정리
- 기본구조
  ```
  flask.app
  ㄴ __init__.py
  ```
- 기본적으로 사용할 땐 `FLASK_APP`이라는 환경변수를 지정하고 사용해야한다.
- EX: export FLASK_APP={ 앱이름 }
- 앱을 실행할 때는 `flask run` ! 

## 라우트
- 라우팅이라고 쓰이는 보편적인 개념은 특정 포인트에 들어왔을 때 어떤 방에 들어갈 것인지를 지정하는 것
- FLASK 에서는 웹 어플리케이션의 엔드포인트를 설정하는 것
- Flask 에서는 기본포트를 5000으로 사용한다.
```python
# __init__.py

from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello World!'
```

- `@app.route('/')` 은 app의 주소 끝에 `/`에 접속했을때 실행하라는 것 : ex) 127.0.0.1:5000/
- 현재 배우는 라우트의 개념은 엔드포인트(endpoint)를 어떻게 설정하게 되는 것
- 기본 URL 뒤에는 슬래시(/)가 붙어어야함
- 예를 들어 `@app.route(/bsch0111)` 처럼 슬래시를 부텽줘야지 오류가 실행되지 않음


## HTTP Request 
- Flask 의 라우트 데코레이터를 사용하게 되면 GET,HEAD, OPTIONS 라는 메소드를 사용할 수 있음
- `method` 라는 인자를 추가해서 POST, PUT, PATCH, DELETE 등 다른 메소드를 사용할 수 있음
- 예시  `@app.route('/user', methods=['POST'])`

## 세부 엔드포인트
```python
@app.route('/name/',defaults={'username': ''})
@app.route('/name/<username>')
def user(username):
```
- 엔드포인트를 이용해 파라미터를 전달해 줄 수 있음
- default 는 기본설정


## 블루프린트
- 라우터를 묶어서 사용할 수 있도록
```python
blueprint = Blueprint('blue',__name__,url_prefix='/blue')
```
- blue 라는 블루프린트를 /blue 라고 불린다면 사용하도록 설정

```python
@blueprint.route('/name')
def get_name():
  return "hi"
```
- `/blue/name` 이라고 연결되면 사용할 수 있도록 지정

### 블루프린트로 지정한 값을 사용하기 위해선 !


- `__init__.py` 파일에 등록해줘야 사용할 수 있음 ! 

```python
app.register_blueprint(blueprint,url_prefix='/blue')
```

## APPLICATION FATORY

app 생성하는 과정을 하나의 함수에 넣어두고 실행하는 것
```python

from flask import FLASK

def create_app():
  app = FLASK(__name__)

  # 불루프린트도 하나의 함수에서 지정하면서 ㅅ사용
  from blueprint_path import blueprint
  app.register_blueprint(blueprint)

if __name__ == "__main__":
  app = create_app()
  app.run()

```

