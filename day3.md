# DAY 3
---
<작업트리> ---- <스테이지> ---- <저장소>

git init 시 작업트리 생성

git add로 작업한 파일 스테이징

git commit으로 스테이지 한 내용 저장소에 저장

tracked -> 한 번 이상 commit한, 추적 중인 파일
untracked -> 새로 생성해서 한 번도 commit한 적 없는 파일

---
main branch는 작업하는 게 아니다!!
main은 병합용도로 써라
새로 기능을 만들어야 할때는 branch를 만들어서 병합해가면서 하는 것이 근본!

### 병합의 종류
##### git merge [sub]: 병합 명령어

* Fast-Forward: 빨리감기 병합
  sub에서 작업한걸 main에 덮어쓰는 방식이 아닌,
  main이 작업을 안했다는 가정하에 HEAD(가장 최근)가 sub의 HEAD를 가르키게 하는 것

* 병합: 
  A, B에서 각각 다른 파일을 작업 후 병합하면
  알아서 각각 다른 버전으로 적용되서 합쳐짐

* 병합충돌: 
  같은 파일을 같이 수정했을 경우 발생하는 충돌

---
### Github
*git의 원격 저장소를 제공하는 클라우드*
*저장소 기능 및 추가 기능 제공 (CI/CD - Github Action)*
- $git remote add origin [URL]: origin이라는 이름으로 해당 URL을 추가한 것
- $git remote -v: 원격 연결 상태 확인
- $git remote: 원격 저장소 별칭 보기
- $git remote rm origin: 원격 연결 끊기
- -u: upstream, $git push -u origin hotfix - origin(원격 저장소)에 hotfix 브랜치가 생성됨.

**원격에서 병합처리 - Pull Request(PR)**

- $git branch: -r 리모트 모음 보기, -a 원격 브랜치 보기
- $git push main --delete sub: 원격 branch 삭제 명령, 
- $git fetch -p main: 수정사항을 다시 불러옴. *에러났을 때 해결 방법중 하나


---
### 가져오기
- $git fetch: 커밋정보만 가져옴
- $git pull (git fetch + 로컬에서 병합)