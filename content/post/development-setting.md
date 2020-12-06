---
title: "초기 맥북 개발환경 구성"
date: 2020-12-04T01:14:14+09:00
Description: ""
Tags: ["개발환경구성"]
Categories: []
DisableComments: false
---

# 초기 맥북 개발환경 구성

- 언어 :  Python
- 쉘 : Fish Shell
- Python 가상환경 : anaconda
- 패키지 설치 프로그램 :brew, cask
- 에디터 : vscose
- 터미널 : iterm2

## 쉘 Fish Shell
"I hate configuration, and combing hundreds of git repos for bashfiles and find what works for me" : 참고한 블로그 글
- 난 초보자니까 자동완성이 되서 사용하도록 하겠음
- zsh + oh my zsh 같은 플러그인도 좋다고한다.
 
- 참고 : Fish and Term2 설치 기록 포스팅 자료
- https://lobster1234.github.io/2017/04/08/setting-up-fish-and-iterm2/l

```bash
 chsh -s /usr/local/bin/fish
 -> fish shell로 default shell을 바꿈
```
fish shell config 파일의 위치 
- cat  ~/.config/fish/fish_variables

- omf : 여러 fish shell 테마 패키지 다운로드 플러그인
https://github.com/oh-my-fish/oh-my-fish/blob/master/docs/Themes.md
패키지 목록 
  - omf install : 설치된 패키지 목록
  - omf install 테마명 : 테마 설치
  - omf theme 테마명                              

- Fish 쉘 명령어 : https://okky.kr/article/454099

## Python 가상환경 anaconda

pyenv-virtualenv 를 사용하면 좋다고 하지만
수강생들이 사용하는 conda를 설치해서 시행착오를 겪어보도록 하겠음
 
- 따라한 Python 설치 블로그
https://medium.com/ayuth/install-anaconda-on-macos-with-homebrew-c94437d63a37
난 fish shell 을 쓰기 때문에 환경변수 설정을 fishshell로  했다

- Fish shell 환경변수 수정방법
- https://fishshell.com/docs/current/tutorial.html#path
- 예시 : set PATH /usr/local/bin /usr/sbin $PATH
- 적용 : set PATH /usr/local/anaconda3/bin $PATH
- 터미널을 껏다 키면 적용안됨

- 영구적으로 적용할때는 다음의 예시를 사용
- 예시 : set -U fish_user_paths /usr/local/bin $fish_user_paths
- 적용 : set -U fish_user_paths /usr/local/anaconda3/bin $fish_user_paths



## 패키지 설치 프로그램 brew

공식 홈페이지(설치) : https://brew.sh/index_ko
Homebrew 관련 좋은 글이 있어서 가져와봄 
(https://m.blog.naver.com/PostView.nhn?blogId=sarang2594&logNo=221246170677&proxyReferer=https:%2F%2Fwww.google.com%2F
)

2. Homebrew에서 설치한 패키지들은 어디에 설치될까?

기본적으로 brew install 명령어를 통해 설치된 패키지는 /usr/local/Cellar 경로에 저장이 된다.

터미널에서 cd 명령으로 위 경로로 이동하고 ls로 목록을 보면 아래와 같이 설치된 패키지들이 보인다. 

4. Homebrew Cask 설치하기

Homebrew는 성공적으로 설치 완료하였다. 그런데 뭔가 아쉽다. 왜냐하면 Homebrew만 설치해서는 우리가 일반적으로 쓰는 GUI 기반의 어플리케이션 (ex. 크롬, atom 등)을 설치할 수 없다. 이런 어플리케이션을 설치하려면 Cask라는 친구도 설치해줘야 한다. 

```
brew install cask
```

## 에디터 : vscose

플러그인으로 한국어 팩(korean) 설치
```
brew cask install visual-studio-code
```
 

## 터미널 : iterm2

- 쉘 중지하고 싶을 때 ctrl + c 프로세스를 중단하려는 명령어
- ctrl + d  터미널 로그아웃, 터미널에서 사용중인 모든 프로세스가 종료됨 위 방법이 동작하지 않을때  사용
- 제일 마지막으로 중지하고 싶은 명령은 ctrl + w 