---
title: "Blog_tab_resize"
date: 2020-12-05T01:47:19+09:00
Description: ""
Tags: ["hugo tab size","hugo column size"]
Categories: ["blog"]
DisableComments: false
---

# hugo anatole 테마 만지기
- hugo anatole 테마 기본은 옆의 탭이 너무 길다.
- https://github.com/lxndrblz/anatole/
- 줄이고 싶다.

# 구글 질문
- hugo anatole column size
- -> https://blog.ryanwcummings.com/posts/hugo-width-adjustment/
    - 이 테마는 themes/hyde-hyde/assets/scss/hyde-hyde/_variables.scss 이 경로에 css 파일이 있다.
- 비슷한 경로에 수정할 css 파일 확인


# hugo server -d
- 로컬서버를 띄우고 크롬 개발자 모드를 통해, 수정할 element 명 확인
- css 에서 해당 element 수정