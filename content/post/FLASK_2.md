---
title: "FLASK_정리2"
date: 2021-03-22T02:11:40+09:00
Description: ""
Tags: ['python','flask']
Categories: ['python','flask']
DisableComments: false
---

## RENTER_TEMPLATE
```python

@app.route('blue')
def main():
    return render_template('blue.html')
```
- templates 폴더 기준으로 `blue.html`이라는 파일을 찾아서 임베드 시켜줌

