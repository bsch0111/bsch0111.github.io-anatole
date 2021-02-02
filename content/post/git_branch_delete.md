---
title: "Git_branch_delete"
date: 2021-02-03T01:29:50+09:00
Description: ""
Tags: ['git']
Categories: ['git']
DisableComments: false
---

> 참고 : https://thdev.tech/git/2016/12/19/Git-Branch-Name-Change/

git branch -m의 명령어 뒤에 변경전_branch_name과 새로운_branch_name 을 작성
```
git branch -m python_v 
```
기존 브런치 삭제
```
git push origin :python_v
```
새 브런치 push
```
git push --set-upstream origin DSFT01 
```