# Git
## Git이란?
### 초기 설정
- 개행 문자 설정
```bash
$ git config --global core.autocrlf true
```
- 사용자 정보 설정
  - commit(버전 생성)을 위한 정보 등록
  - global을 빼면 그 깃 폴더에서만 적용
```bash
$ git config --global user.name 사용자이름
$ git config --global user.email 사용자이메일
```
- 설정 정보 확인
```bash
$ git config --list
$ git config --global --list
```
### 저장소 생성
- 현재 프로젝트에서 변경사항 추적(버전 관리)을 시작
- Git을 사용할 프로젝트 폴더로 이동 후
```bash
$ git init
```
- 위치를 지정해서 생성(폴더가 존재하지 않으면 생성도 함)
```bash
$ git init 상대경로폴더위치
```
---
### 파일 생성
- 모든 파일의 변경사항을 추적하도록 지정(stage)
```bash
$ git add .
```
- 특정 파일의 변경사항을 추적하도록 지정(stage)
```bash
$ git add 파일이름
```
- 특정 파일을 잘못 add 했을 때
```bash
$ git reset HEAD 파일이름
```

### 저장소 반영
- 메시지(-m)와 함께 버전을 생성
```bash
$ git commit -m "커밋메시지"
```
- 커밋 메시지 수정
```bash
$ git commit --amend
$ git commit --amend -m "수정할메시지"
```

### 관리 상태 확인
- `git status`: staging file들의 상태 확인
- `git log`: git repository에 존재하는 history 확인
  - `git log -p -숫자`: 상위 숫자만큼의 각 commit의 수정 결과를 보여주는 diff와 같은 역할
  - `git log --stat`: 어떤 파일이 commit에서 수정되고 변경 되었는지, 파일 내 라인이 추가되거나 삭제 되었는지 확인
  - `git log --pretty=oneline`: 각 commit을 한 줄로 보여줌
  - `git log --graph`: commit 간의 연결 된 관계를 아스키 그래프로 보여줌
  - `git log -s 찾는텍스트`: 코드에서 추가되거나 제거된 내용 중 특정 텍스트가 포함 되었는지 확인 
- `git diff`: commit된 파일 중 변경 된 사항을 비교할 때
---
## 가지 치기
### Branch
- 독립적으로 어떤 작업을 진행하기 위한 개념
- 배포할 수 있는 수준의 main branch와 기능 추가나 버그 수정과 같은 단위 작업을 위한 topic branch가 있음
- branch 생성
```bash
$ git branch 생성할브랜치이름
```
- branch 목록 확인
```bash
$ git branch
$ git branch -a
```
- branch 전환
```bash
$ git checkout 브랜치이름
```
- 특정 버전으로 이동
```bash
$ git checkout 특정해쉬값
```
### Merge
0. master branch로 이동
1. merger를 시도
```bash
$ git merge 병합할브랜치이름
```
cf) fast forward: master branch에선 변경 없이 다른 branch에서만 업데이트되어 merge하는 것
- 병합된 branch 확인
```bash
$ git branch --merged
```
- branch 삭제
```bash
$ git branch -d 삭제할브랜치이름
```

### conflict 해결
- 같은 파일을 가지고 수정했을 때 어떤 파일을 병합해야 하는지 몰라서 충돌 발생
0. `git status`: 무슨 파일이 충돌 했는지 확인
1. 충돌한 파일 확인
2. `git add`, `git commit` 후에 다시 merge 해줌

ex) branch1, branch2가 충돌
0. head->branch1
  - 파일 확인 및 `git add`, `git commit`
1. head->branch2
  - merge branch1
2. head->master
  - merge branch1
---
## 원격 저장소
### 받아오기
```bash
$ git clone 받아올원격저장소주소
$ git clone .
```
- 원격 저장소 추가
  - 원격 저장소 이름 origin을 변경할 수도 있음
```bash
$ git remote add origin 받아올원격저장소주소
```

- 연결된 원격 저장소 확인
```bash
$ git remote
$ git remote show origin
```

- 원격 저장소 삭제
  - 주소가 변경되었거나, 필요 없어진 저장소는 삭제
```bash
$ git remote rm 삭제할저장소이름
```

### 원격 저장소 동기화
- pull: 원격 저장소에서 데이터 가져오기 + 병합
  - `git pull`
- fetch: 원격 저장소에서 데이터 가져오기
  - `git fetch` + `git merge origin/master`

- 저장소 발행
  - 저장소에서 작업한 내용을 원격 저장소에 반영함
  - 다른 사람이 먼저 push한 상태에서는 push 할 수 없음
  - 다른 사람이 작업한 것을 merge 부터 해야 함
  - 그 후, `git push origin master`로 변경된 사항을 원격 저장소에 전달

```bash
$ git remote add origin(또는다른원격저장소이름)
$ git fetch
$ git merge origin/master
$ git push origin master
```

### Origin
- `git remote add origin ~`: 원격 저장소의 단축 이름을 origin으로 지정
- `git remote -v`: 지정한 저장소의 이름과 주소를 함께 볼 수 있음
