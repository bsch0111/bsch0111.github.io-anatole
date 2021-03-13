---
title: "Orm에_대해서"
date: 2021-03-13T22:41:48+09:00
Description: ""
Tags: ["ORM", "python"]
Categories: ["python"]
DisableComments: false
---

### ORM (Object_Relational Mapper)

**장점**

- 현재 사용하고 있는 언어만 사용해도 됨
- 데이터베이스 시스템으로부터 분리가 됨
- 직접 작성하는 SQL 쿼리문이 없고 더 높은 성능의 SQL 쿼리문을 작성할 수 있습니다.

**단점**

- 데이터베이스와 바로 연결하는 것보다 초기설정이 더 많아지거나 복잡해질 수 있습니다.
- 내부 작동에 대한 충분한 이해가 없는 경우 해결이 힘들 수 있습니다.
- 데이터베이스에 직접 쿼리문을 보내는 것이 아니기 떄문에 성능 저하가 발생합니다.

## SQLAlchemy (ORM 의 기능을 제공하는 Python 라이브러리)

### Core

- 데이터베이스와 상호작용

### 엔진

```python
from sqlalchemy import create_engine

engine = create_engine("데이터베이스 주소")

#engine = create_engine("sqlite:///:memory:")

# 주위
# - :// 다음에 / 가 하나가 오면 현재 디렉토리부터 상대적인 경로, // 처럼 두개가 있다면 절대적인 경로
# - :memory: -> 메모리에서 임시적인 데이터베이스를 사용한다는 뜻

```

### 매핑(Mappaing)

- 데이터베이스의 구조와 코드상의 구조를 연결하는 것
- 특정 테이블이 데이터베이스 상에 존재한다면 코드 상에서도 해당 테이블과 연결될 수 있도록 테이블을 구현하는 것

`declarative_base()`

- `base class` 를 리턴
- `base class` 를 상속받은 클래스는 자동으로 ORM이랑 연결지어서 사용됨

```sql
CREATE TABLE user (
    id INTEGER PRIMARY KEY,
    name STRING,
    age INTEGER
)
```

```python

from sqlalchemy.orm import declarative_base

base = declarative_base()

from sqlalchemy import Column, Integer, String

class User(base):
    __tablename__ = 'user'

    id = Column(String, primary_key=True)
    name = Column(String)
    age = Column(Integer)

    # id = Column(name = 'id', Integer, primary_key=True)
    # name = Column(name = 'name', String)
    # age = Column(name = 'age', Integer)


    def __repr__(self):
        return f"USER id : {self.id}, name : {self.name}, age : {self.age}"
```

- 클래스의 이름을 소문자로 변경한 테이블과 매핑
- `__tablename__`을 사용해도 좋지만, 클래스 이름으로 매핑시키는게 더 좋아보임

### 매핑한 내용을 데이터베이스와 연결 ( 스키마 생성 )

` base.metadata.create_all(engine)`

## 세션 (Session)

```python
from sqlalchemy.orm import sessionmaker
Session = sessionmaker(bind=engine)

# 후에 연결도 가능
# Session = sessionmaker()
# Session.configure(bind=engine)
```

- 이후 세션을 통한 작업

### Create : 데이터 추가

```
ed_user = User(id='ed', name='Ed Jones', age=19)
Session.add(ed_user)

<!-- Session.add_all([
    User(id='ed', name='Ed Jones', age=19),
    User(id='wd', name='Wendy', age=19),
    User(id='fd', name='Fred', age=19),
]) -->
```

### 조회

```python
 our_user = session.query(User).filter_by(name='ed').first()

#  >> ed_user == our_user (값 비교)
#  >> TRUE
#  >> ed_user is our_user (주소 비교)
#  >> TRUE
```

```python
for instance in session.query(User).order_by(User.id):
    print(instance.name, instance.fullname)

for id, name in session.query(User.id, User.name):
    print(id, name)

for row in session.query(User, User.Uname).all():
    print(row.User, row.name)

#LIMIT
for u in session.query(User).order_by(User.id)[1:2+1]:
    print(u)

# Filter
for name in session.query(User.name).filter_by(name='Ed Jones'):
    print(id)
# Filter : SQL 보다 유연하게 사용가능 ( Python 연산자 모두 가능)
for name in session.query(user.name).filter_by(User.name=='Ed Jones')

for user in session.query(User).filter(User.id=='ed')\
.filter(User.name=='Ed Jones')

for user in session.query(User).filter(User.name.like('%ed%'))
```

### 세션을 데이터베이스에 적용하고 싶을때

`Session.commit()`

```

```
