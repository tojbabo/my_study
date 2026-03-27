# 2일차 - Git

---

### Basic Operation

<span style="background-color:#fdd;">작업 디렉토리 ------------ 스테이지 ------------로컬 저장소</span>

$git add: 새로 추가된 파일을 스테이징(tracking)함

$git commit: 변경 사항을 로컬 저장소로 저장함
- --amend: 옵션을 추가해서 commit 메시지를 변경 가능함.
- -am: 변경된 파일 추가 및 메시지 지정
  
$git diff: 작업 디렉터리와 로컬 저장소 비교
- -staged: 스테이징 된 애만 비교

$git log: commit 로그를 볼 수 있다.
- --oneline옵션으로 간단하게 쭈루룩 볼 수 있다.
- $git diff [hash] 해쉬 값으로 특정 커밋과 비교해볼 수 있다

$git restore [파일명]: 커밋 이전상태 되돌리기
- --staged: git add 되돌리기

$git reset [option] [hash]: 커밋 이후 작업 되돌리기
*커밋 로그도 지워지기 때문에 조심해야함*
- --soft : git commit 되돌리기
- --mixed: git add 전까지 되돌리기
- --hard : 작업 디렉터리 수정 전까지 되돌리기

$git revert [hash]: 기존 새로운 커밋을 만들고 해당 위치로 이동, one > two > three > four(one)
- --abort : 잘 안되면 명령어를 취소해버리자

---

### Base

로컬 저장소: .\.git\object에 해시값 앞에 두 글자로 된 폴더에 잘 저장되어있다.

.gitignore 파일을 써서 추적하지 않을 파일을 명시할 수 있다.
<span style=background-color:#dfd> **gitignore에 명시해도 적용이 안되는 경우가 있는데, 이땐 cache를 지워줘야 한다.** </span>
https://www.toptal.com/developers/gitignore < 홈페이지를 통해 자동으로 만들어 준다!

---

### Branch

이전엔 default branch는 master였다. > 요즘은 main으로 바뀜.
git init 시 main branch로 자동 설정됨

*각 branch는 독립적임. branch 복사 시 reference가 아닌, copy된 branch가 생성되는 것!*

- $git branch: check the branch list
- $git branch [name]: create new branch
- $git branch -d [name]: delete the branch
- $git switch [name]: switch current branch (=git checkout [name] - oldy operation)
  - -c: with this option, switch branch after create
- $git branch main..[name]: check the differnce on [name] from main
- $git merge [name]: merging branch [name] from current
  - done this job. delete the sub branch

