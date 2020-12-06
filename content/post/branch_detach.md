---
title: "부모 레포지토리와 submodule 레포지토리의 포인트가 달라서 생기는 문제"
date: 2020-12-05T01:28:20+09:00
Description: ""
Tags: ["submodule","detach"]
Categories: ["git"]
DisableComments: false
---

# 부모 레포지토리와 submodule 레포지토리의 포인트가 달라서 생기는 문제
- git log
- 커밋 포인터 중에서 HEAD 와 origin/main 이 다른 것을 확인할 수 있다
```bash
commit 81e8e894f15f76aa85ba72846f125b33007c7a30 (HEAD)
Author: bsch0111 <bsch0111@naver.com>
Date:   Sat Dec 5 00:44:32 2020 +0900

    has-submodules

commit 167d77dc73841b63e7983b1ba3b3207e24b02052
Author: bsch0111 <bsch0111@naver.com>
Date:   Sat Dec 5 00:32:48 2020 +0900

    submodules

commit 3af11a9cd07b40de3b89e7543088250f567cf66b
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Sat Dec 5 00:23:38 2020 +0900

    submodule

commit 5024e7c51cb95d2553544e7c7dc0a5cc957c8343 (list)
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Fri Dec 4 23:59:20 2020 +0900

    submodule 가지고 있는 repo clone 시 문제점

commit 58296efe75968307fa199b17b576c131610058b2
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Fri Dec 4 23:45:16 2020 +0900

    git 궁금증 포스팅

commit a562180084d92b666a0f4157acfcf01be0ef1f45
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Fri Dec 4 23:43:21 2020 +0900

    git 궁금증 포스팅

commit 1e4b0195be45dcfb1bcd621d2539c2c1693243c8
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Fri Dec 4 23:42:04 2020 +0900

    git 궁금증 포스팅

commit 9fe889c7860ee03e64bc428aa6b8db0da6be9b6f
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Fri Dec 4 23:41:24 2020 +0900

    git 궁금증 포스팅

commit b4d00b8578501c0d48ebd8d15d3ee02da4103d50
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Fri Dec 4 23:40:47 2020 +0900

    git 궁금증 포스팅

commit 3a21be82f4a336daaa6d4ff53b3ad23e10c92a81
Author: bsch0111 <bsch0111@bsch0111ui-MacBookPro.local>
Date:   Fri Dec 4 23:38:38 2020 +0900

    git 궁금증 포스팅

commit 97aa2e682555d27cff7d47b01af728957309ef63 (origin/main, origin/HEAD, main)
Author: bsch0111 <bsch0111@naver.com>
Date:   Fri Dec 4 01:27:53 2020 +0900

    개발환경 구성 포스팅
```

## 해결 방법
- 참조 : GitHub : 커밋 시 'HEAD detached at SHA-1.. ' 메시지가 나오며 push가 되지 않을 때
출처: https://geoseong.tistory.com/50 [진화하는개발자]

- 임시 브런치를 생성해서 현재 HEAD 의 위치를 할당한 다음, origin/main 브런치와 merge하여 하나의 포인터를 연결 짓도록 변경
1. 임시 브런치 (solve_detach) 생성 & 뒤 해싱은 HEAD 커밋의 해싱 8자리
- checkout -b 옵션 : 새 브런치 생성
```bash
 ~/D/h/b/public  ➦ 81e8e89  git checkout -b solve_detach 81e8e89                    12.2s  토 12/ 5 01:12:35 2020
Switched to a new branch 'solve_detach'
```

2. origin/main 과 solve_detach 의 현재 포인트 확인

- origin/main 브런치 checkout 후 포인터 확인 
```bash

 ~/D/h/b/public   solve_detach  git checkout main                                          토 12/ 5 01:12:53 2020
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
 ~/D/h/b/public    git status                                                              토 12/ 5 01:13:04 2020
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
 ~/D/h/b/public    git log -2                                                              토 12/ 5 01:13:12 2020
commit 97aa2e682555d27cff7d47b01af728957309ef63 (HEAD -> main, origin/main, origin/HEAD)
Author: bsch0111 <bsch0111@naver.com>
Date:   Fri Dec 4 01:27:53 2020 +0900

    개발환경 구성 포스팅

commit eec7b2878f10f5d188fca49a2489db3578d2f51b
Author: bsch0111 <bsch0111@naver.com>
Date:   Fri Dec 4 01:23:02 2020 +0900

    개발환경 구성 포스팅
```
- solve_detach 브런치 checkout 후 브런치 확인
```bash
 ~/D/h/b/public    git checkout solve_detach                                               토 12/ 5 01:13:50 2020
Switched to branch 'solve_detach'
 ~/D/h/b/public   solve_detach  git log -2                                                 토 12/ 5 01:14:30 2020
commit 81e8e894f15f76aa85ba72846f125b33007c7a30 (HEAD -> solve_detach)
Author: bsch0111 <bsch0111@naver.com>
Date:   Sat Dec 5 00:44:32 2020 +0900

    has-submodules

commit 167d77dc73841b63e7983b1ba3b3207e24b02052
Author: bsch0111 <bsch0111@naver.com>
Date:   Sat Dec 5 00:32:48 2020 +0900

    submodules
```
- 생성된 branch인 solve_detach 가 최신 커밋을 포인트 하고 있는걸 알 수 있음

3. origin/main 브런치와 solve_detach 브런치 merge

```
 ~/D/h/b/public   solve_detach  git checkout main                                          토 12/ 5 01:14:35 2020
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

~/D/h/b/public    git merge solve_detach                                              토 12/ 5 01:14:51 2020
Updating 97aa2e6..81e8e89
Fast-forward
 categories/git/
```

4. 커밋 포인트 확인후 HEAD 가 main으로 잘 되어있으면 push
```bash
 ~/D/h/b/public   +  git log -2                                                            토 12/ 5 01:15:04 2020
commit 81e8e894f15f76aa85ba72846f125b33007c7a30 (HEAD -> main, solve_detach)
Author: bsch0111 <bsch0111@naver.com>
Date:   Sat Dec 5 00:44:32 2020 +0900

    has-submodules

commit 167d77dc73841b63e7983b1ba3b3207e24b02052
Author: bsch0111 <bsch0111@naver.com>
Date:   Sat Dec 5 00:32:48 2020 +0900

    submodules
 ~/D/h/b/public   +  git push origin main                                                  토 12/ 5 01:15:12 2020
Enumerating objects: 116, done.
Counting objects: 100% (116/116), done.
Delta compression using up to 12 threads
Compressing objects: 100% (90/90), done.
Writing objects: 100% (100/100), 16.01 KiB | 2.29 MiB/s, done.
Total 100 (delta 68), reused 0 (delta 0)
remote: Resolving deltas: 100% (68/68), completed with 12 local objects.
To https://github.com/bsch0111/bsch0111.github.io.git
   97aa2e6..81e8e89  main -> main
```

5. 사용한 브런치 삭제 & 쓸모없는 브런치 삭제
```bash
 ~/D/h/b/public    git branch                                                         5s  토 12/ 5 01:15:28 2020
  list
* main
  solve_detach
 ~/D/h/b/public    git branch -d list                                                      토 12/ 5 01:26:37 2020
Deleted branch list (was 5024e7c).
 ~/D/h/b/public    git branch -d solve_detach                                              토 12/ 5 01:26:46 2020
Deleted branch solve_detach (was 81e8e89).
```
