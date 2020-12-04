---
title: "Problem When Repository Has Submodule"
date: 2020-12-04T23:55:06+09:00
Description: ""
Tags: ["git","submodule"]
Categories: ["git"]
DisableComments: false
---

# Clone 할 레포지토리가 submodule을 포함하고 있을 떄

## 문제점 
- 이전에 로컬 저장소에서 push 할 때 하나의 저장소 밑에 하나의 저장소가 submodule로 되어 있음

### 궁금증
- 다시 클론해서 가져올 때 submodule 이 지정되어 있는가?
- submodule 이 지정되어 있지 않다면 어떻게 지정하는가?

### git clone [path] 를 통한 해결 시도
* submodule 이 지정이되어있지만 다음과 같은 에러가 발생함
  - fatal: in unpopulated submodule 'public'
  - 단순 git clone 으로 레파지토리를 복사해서는 안됨.

### 질문을 google 으로 .. 
	- submodule 이 있는 git repo clone 후 작업하고 push가 안될 때
    - git clone submodule  
    - https://stackoverflow.com/questions/3796927/how-to-git-clone-including-submodules
    - 서브 모듈이 있는 레포지토리는 부모 레포를 clone 할때 —recurse-submodules를 넣어주면 서브 모듈에 대한 clone과 init 을 잘해준다.
    ```bash
       --recurse-submodules[=<pathspec]
           After the clone is created, initialize and clone submodules within based on the provided
           pathspec. If no pathspec is provided, all submodules are initialized and cloned. This option
           can be given multiple times for pathspecs consisting of multiple entries. The resulting clone
           has submodule.active set to the provided pathspec, or "." (meaning all submodules) if no
           pathspec is provided.

           Submodules are initialized and cloned using their default settings. This is equivalent to
           running git submodule update --init --recursive <pathspec> immediately after the clone is
           finished. This option is ignored if the cloned repository does not have a worktree/checkout
           (i.e. if any of --no-checkout/-n, --bare, or --mirror is given)
    ```bash

