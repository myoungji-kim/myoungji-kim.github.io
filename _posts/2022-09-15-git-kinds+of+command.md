---
title: "Git에서 자주 사용하는 명령어들"
excerpt: "Git. 나를 위한 명렁어 모음"

categories:
  - git
# tags:
#   - [tag1, tag2]

permalink: /git/kinds+of+command/

toc: true
toc_sticky: true

date: 2022-09-15
last_modified_at: 2022-09-15

---

### 🧩 <b>명령어 모음</b>

#### <b>reset 관련 명령어</b>
* git reset HEAD^ : 최신 커밋 삭제 <br>

#### <b>diff 관련 명령어</b>
> Working Directory -> Staging Area -> Repository
* git diff : working directory와 statging area 사이의 차이 확인 <br>
* git diff HEAD : Working Dicrectory + Staging Area 와 Repository 차이 비교 <br>
* git diff --staged : Staging Area와 Repository HEAD 커밋 사이의 변경사항을 확인하기 위한 용도


#### <b>push 관련 명령어</b>
* git push \<remotename> \<commit SHA>:\<remotebranchname> <br> : 원하는 커밋까지만 push하기


<br><br><br>

git stash
git fetch --prune
git switch feature/203
git pull origin feature/203
git switch -c feature/203-2
git stash pop
git stash list