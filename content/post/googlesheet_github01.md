---
title: "google Sheet에 Github Repo 정보 가져오기"
date: 2021-01-03T23:39:36+09:00
Description: ""
Tags: [google_sheet,github_API]
Categories: [github_API]
DisableComments: false
---
# google Sheet에 Github Repo 정보 가져오기

- [Import GitHub Data to Google Sheets](https://mixedanalytics.com/knowledge-base/access-github-data-in-google-sheets/) 의 글을 따라 시도해보았습니다.


## [Import GitHub Data to Google Sheets](https://mixedanalytics.com/knowledge-base/access-github-data-in-google-sheets/) 따라하기

- 예제는 https://github.com/octocat/Hello-World/ 의 데이터를 사용

- 업무에서 사용하는 레포지토리와 다른 점

  - 업무에서 활용하는 레포지토리는 Private로 되어 있음
  - Priavte 는 권한작업을 해줘야 할 것임

  

- 세 가지 정보를 수집해보겠음

  - Repository Pull Request
  - Commit Messages in Pull Request
  - Raw Data related with Commit



### Step 1) 빈 구글 시트 생성

![image-20210103192901803](https://i.imgur.com/0Wo9m7M.png)

### Step 2) Google Sheet Add-ons을 이용해서 API Connector 설치

- Add-ons --> Get Add-ons --> API Connector install

![img](https://i.imgur.com/RNYKaRr.png)

![img](https://i.imgur.com/erqqdLD.png)

### Step 3) API Connector 에서 GITHUB API 사용할 수 있도록 연결

- Add-ons -> API Connector -> Manage Connections -> Github Connect

![img](https://i.imgur.com/W34pttr.png)

![img](https://i.imgur.com/ImQ0PAx.png)

![img](https://i.imgur.com/K4tmKSn.png)

![img](https://i.imgur.com/2GML3xh.png)



### Step 4) REQUEST API 생성

- pull requests list

```shell
https://api.github.com/repos/octocat/hello-world/pulls
```

- 특정 pull requests

```
https://api.github.com/repos/octocat/hello-world/pulls/796
```

- 특정 pull requests 안에 있는 commit list

```
https://api.github.com/repos/octocat/hello-world/pulls/796/commits
```





### Step 5) Github Data를 Sheet로 가져오기

- Add-ons --> API Connector --> Open

- Create 탭으로 가서 작성할 API에 대한 자료 입력
  - method : GET
  - API URL path : https://api.github.com/repos/octocat/hello-world/pulls
  - Authentication : GITHUB
  - Destination sheet : 우선 Set Current로 지정
  - REQUEST NAME 지정 : Example_REQUEST
  - RUN 혹은 SAVE 지정

- 총 30개의 REQUEST 에 대한 데이터를 저장함

![img](https://i.imgur.com/sbTbgMd.png)

![img](https://i.imgur.com/9dLqi6d.png)



### Step 6) Run ! 

![img](https://i.imgur.com/YeasdAd.png)