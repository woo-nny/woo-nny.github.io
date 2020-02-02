---
layout: page
title: Git
description: >
  깃(Git)은 컴퓨터 파일의 변경사항을 추적하고 여러 명의 사용자들 간에 해당 파일들의 작업을 조율하기 위한 분산 버전 관리 시스템이다.
hide_description: true
---

깃(Git)은 컴퓨터 파일의 변경사항을 추적하고 여러 명의 사용자들 간에 해당 파일들의 작업을 조율하기 위한 분산 버전 관리 시스템이다.

## Git 순서
{:.no_toc}
0. this unordered seed list will be replaced by toc as unordered list
{:toc}

## 커밋
변경 사항 덩어리
CLI -> git commit -m "메시지내용"

## 푸시
커밋을 공동(원격)저장소에 올리다
CLI -> git push origin master

## 풀
다른 사람이 개발한 코드(커밋)을 내 컴퓨터로 받는다.
CLI -> git pull

## 브랜치
한 저장소에서 다른 개발자랑 같이 작업할고 싶을때 브랜치 만듬
-한 줄로 쌓던 커밋을 n줄로 쌓을 수 있게 만들어 준다.
CLI -> git branch branch-name

## 병합
브랜치에서 작업이 끝나고 코드를 합친다. 브랜치+브랜치
CLI -> git merge branch-name

## 풀 리퀘스트
병합 요청 편지(병합하기 전에 다른 개발자들에게 리뷰&컨펌)

**NOTE**: 알아두면 편리한 명령
~~~bash
1.git Stash -> 하던 작업 임시로 저장하기
  git stash save
  git stash list
  git stash apply ->최근 적용
  git stash apply <stash  이름>
  git stash drop -> 최근 삭제
  git stash drop <stash 이름>
2.Discard(변경사항 삭제) / Remove(파일 삭제)
  Discard -> 아직 commit을 하지 않은 자료를 최종버전의 commit으로 되돌리는 기능
  Remove -> 해당 파일을 삭제 하는 것
3.Cherry pick
  cherry-pick -> 다른 브랜치에 있는 커밋을 선택적으로 내 브랜치에 적용시킬 때 사용하는 명령어
  git cherry-pick <커밋> <커밋>...
4. Amend last commit
5. rebase
~~~

## 헷갈림 포인트
~~~
1.Origin 이 붙은것과 안 붙은것?
2. 2 behind 뜻?
3. unstage 와 stage 차이?
4. changes다 없애고 싶을때 방법?
   1. stash / reset / discard(+remove)
5. reset soft/mixed/hard
6. reset, revert 언제 해야하는지?
  reset 더 이상 필요 없어진 commit들을 버릴 수 있습니다. soft, mixed, hard를 선택할 수 있는데 soft는 커밋만 되돌리고 싶을 때, 
  mixed는 지금까지 하던 작업을 그대로 둔 상태에서 내가 원하는 commit으로 돌아가며, 그 때까지의 commit은 모두 사라지는 기능,
  hard는 내가 원하는 commit으로 돌아가면서 그 때까지의 commit이 모두 없어지고 하던 작업도 사라지는 기능
  옵션: hard, mixed, soft
  git reset <옵션> <돌아가고 싶은 커밋>
  revert commit을 지우지 않고 새로운 commit을 추가하면서 내가 원하는 곳으로 되돌아 가는 기능
  git revert <되돌릴 커밋>
~~~

## Git 간편 안내서
`git init`
: 새로운 git 저장소가 만들어진다
`git clone`
: 저장소 받아오기
`git add <파일 이름>`
: 변경된 파일 추가
`git commit -m "설명"`
: 변경 내용을 확정한다.
`git push origin master` 
: 푸시하기 (다른 브랜치로 발행 하려면 master 자리를 변경)
**NOTE**:만약 기존에 있던 원격 저장소를 복제한 것이 아니라면, 원격 서버의 주소를 git에게 알려줘야 한다.
   git remote add origin <원격 서버 주소>
`git checkout -b <브랜치 이름>`
: 브랜치 만들고 갈아탄다
`git checkout master`
: 마스터 브랜치로 돌아온다
`git branch -d <브랜치 이름>`
: 브랜치 삭제
`git pull`
: 여러분의 로컬 저장소를 원격 저장소에 맞춰 갱신한다
`git merge <브랜치 이름>`
: 다른 브랜치에 있는 변경 내용을 현재 브랜치로 병합
`git diff <원래 브랜치> <비교 대상 브랜치>`
: 변경 내용을 병합하기전에, 어떻게 바뀌었는지 비교
`git checkout -- <파일 이름>`
: 실수로 무언가 잘못한 경우, 로컬의 변경 내용을 되돌릴수 있다.

Continue with [Config](config.md){:.heading.flip-title}
{:.read-more}


[upgrade]: upgrade.md
