---
title: "Git에서 자주 사용하는 명령어들"
excerpt: "Git. 나를 위한 명렁어 모음"

categories:
  - Git
# tags:
#   - [tag1, tag2]

permalink: /git/kinds+of+command/

toc: true
toc_sticky: true

date: 2022-09-15
last_modified_at: 2022-09-17

---

#### <b>🧩 reset 관련 명령어</b>
* git reset HEAD^ : 최신 커밋 삭제 <br>
* git reset --hard 'commit number'

---

#### <b>🧩 diff 관련 명령어</b>
> Working Directory -> Staging Area -> Repository <br>

* git diff : working directory와 statging area 사이의 차이 확인 <br>
* git diff HEAD : Working Dicrectory + Staging Area 와 Repository 차이 비교 <br>
* git diff --staged : Staging Area와 Repository HEAD 커밋 사이의 변경사항을 확인하기 위한 용도

---

#### <b>🧩 push 관련 명령어</b>
* git push \<remotename> \<commit SHA>:\<remotebranchname> <br> : 원하는 커밋까지만 push하기
* git push origin +feature/214

---

#### <b>🧩 switch 관련 명령어</b>
* git switch feature/101 : feature/101이라는 브랜치로 이동
* git switch -c feature/101-1 : feature/101-1이라는 브랜치를 생성 후 이동

---

#### <b>🧩 stash 관련 명령어</b>
(stash list에 가급적 아무것도 남기지 말자!)
* git stash
* git stash pop
* git stash list

---

#### <b>🧩 fetch 관련 명령어</b>
* git fetch --prune : commit 된 상태들 불러오기


---

#### <b>🧩 특정 브랜치로 push하고 기존 브랜치 삭제하기</b>
* git switch feature/203-static
* git pull origin feature/203-2
* git push origin feature/203-static
* git push origin --delete feature/203-2
* git branch -D feature/203-2

--- 

#### <b>🧩 cherry-pick 관련 명령어</b>

> 다른 브랜치에 있는 커밋을 선택적으로 내 브랜치에 적용시킬 때 사용하는 명령어

* git cherry-pick 'commit number'

---

#### <b>🧩 기타</b>  
* git log
* git pull origin feature/214 --rebase


