---
layout: post
title: GitHub - Git 브랜치 종류 및 사용법 4가지
subtitle: branch
date: 2023-11-24
author: Warner
header-img: img/bg/post-bg-github-cup.jpg
catalog: true
tags:
  - Github
---

## 4가지 브랜치

- "A successful Git branching model" 이란 컬럼에 소개된 4가지 브랜치 모델
  ![git-model-all.png](/img/post/2023/2023-11-24/git-model-all.png)

## 메인 브랜치 (Main branch)

- 'master' 브랜치와 'develop' 브랜치를 보통 메인 브랜치로 사용

### master

- 'master' 브랜치는 배포 가능한 상태만을 관리, 커밋할 때는 태그를 사용하여 배포 번호를 기록

### develop

- 'develop' 브랜치는 통합 브랜치의 역할
- 평소 이 브랜치를 기반으로 개발 진행
- 모든 기능이 정상적으로 동작할 수 있는 안정적인 상태를 유지
- 배포 가능한 상태라면 'master' 브랜치에 merge
  ![main-branches.png](/img/post/2023/2023-11-24/main-branches.png)

## 피쳐 브랜치 (Feature branch)

**기능 단위**로 분기하여 사용하는 브랜치

- develop 브랜치에서 분기
- develop 브랜치로 merge

### 피쳐 브랜치 사용법

1. 이슈 생성
   ![issue.png](/img/post/2023/2023-11-24/issue.png)
2. feature/#2-issue 이슈 넘버 포함시켜 피쳐 브랜치 생성
   ![createbranch.png](/img/post/2023/2023-11-24/createbranch.png)
3. 기능 개발
   ![add.png](/img/post/2023/2023-11-24/add.png)
4. 커밋 && 커밋 메세지 작성
   ![commit.png](/img/post/2023/2023-11-24/commit.png)
5. push
   ![push.png](/img/post/2023/2023-11-24/push.png)
6. pull request
   ![pull-request.png](/img/post/2023/2023-11-24/pull-request.png)
7. code review
   ![code-review.png](/img/post/2023/2023-11-24/code-review.png)
8. merge
   ![merge.png](/img/post/2023/2023-11-24/merge.png)

code로 작업 할 경우

~~~yaml
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff myfeature
Updating ea1b82a..05e9557
(Summary of changes)
$ git branch -d myfeature
Deleted branch myfeature (was 05e9557).
$ git push origin develop
~~~

![merge-without-ff.png](/img/post/2023/2023-11-24/merge-without-ff.png)

## 릴리즈 브랜치 (Release branch)

- develop 브랜치에서 분기
- develop 브랜치와 master 브랜치로 merge

Release 브랜치에서는 버그를 수정하거나 새로운 기능을 포함한 상태로 모든 기능이 정상적으로 동작하는지 확인한다. Release 브랜치의 이름은 관례적으로 브랜치 앞에 'RB_' 접두어를 붙인다. 이때, 다음 번
Release를 위한 개발 작업은 'develop' 브랜치에서 계속 진행해 나간다.

Release 브랜치에서는 Release를 위한 최종적인 버그 수정 등의 개발을 수행한다. 모든 준비를 마치고 배포 가능한 상태가 되면 'master' 브랜치로 병합시키고, 병합한 커밋에 Release 번호 태그를
추가한다.

Release 브랜치에서 기능을 점검하며 발견한 버그 수정 사항은 'develop' 브랜치에도 적용해 주어야 한다. 그러므로 배포 완료 후 'develop' 브랜치에 대해서도 병합 작업을 수행한다.

### release 브랜치 만들기

~~~yaml
$ git checkout -b release-1.2 develop
Switched to a new branch "release-1.2"
$ ./bump-version.sh 1.2
Files modified successfully, version bumped to 1.2.
$ git commit -a -m "Bumped version number to 1.2"
[release-1.2 74d9424] Bumped version number to 1.2
1 files changed, 1 insertions(+), 1 deletions(-)
~~~

### release 브랜치 종료와 merge

~~~yaml
$ git checkout master
Switched to branch 'master'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2
~~~

~~~yaml
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
~~~

~~~yaml
$ git branch -d release-1.2
Deleted branch release-1.2 (was ff452fe).
~~~

## 핫픽스 브랜치 (Hotfix branch)

- master 브랜치에서 분기
- develop 브랜치와 master 브랜치로 merge
- 브랜치 이름은 hotfix-*

배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우, 'master' 브랜치에서 분기하는 브랜치입니다. 관례적으로 브랜치 이름 앞에 'hotfix-'를 붙인다.
![hotfix-branches.png](/img/post/2023/2023-11-24/hotfix-branches.png)

### hotfix 브랜치 만들기

~~~yaml
$ git checkout -b hotfix-1.2.1 master
Switched to a new branch "hotfix-1.2.1"
$ ./bump-version.sh 1.2.1
Files modified successfully, version bumped to 1.2.1.
$ git commit -a -m "Bumped version number to 1.2.1"
[hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1
1 files changed, 1 insertions(+), 1 deletions(-)
~~~

~~~yaml
$ git commit -m "Fixed severe production problem"
[hotfix-1.2.1 abbe5d6] Fixed severe production problem
5 files changed, 32 insertions(+), 17 deletions(-)
~~~

### hotfix 브랜치 종료와 merge

~~~yaml
$ git checkout master
Switched to branch 'master'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2.1
~~~

~~~yaml
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
~~~