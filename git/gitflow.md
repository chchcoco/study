---
marp: true
---

# git flow 진행 순서

---

# branch 종류
![bg left:40% height:500px](https://techblog.woowahan.com/wp-content/uploads/img/2017-10-30/git-flow_overall_graph.png) 
1. master
    > 제품으로 출시 가능한 브랜치 
2. develop
    > 다음 버전 개발하는 브랜치
3. feature
    > 기능 개발 브랜치
4. release
    > 이번 출시 버전을 준비하는 브랜치
5. hotfix
    > 출시 버전에서 버그를 수정하는 브랜치

---

# 전체적인 방향
- 최초, master 브랜치와 develop 브랜치(상시로 버그 수정 커밋이 추가)가 존재
- 새 기능 추가시 develop에서 feature 브랜치가 생성
    > feature는 항상 develop에서 시작됨
    > 기능추가작업 완료시 develop브랜치로 merge됨
- develop에서 모든 기능 merge완료된 경우 QA진행을 위해 release 브랜치 생성
    > QA 진행과 동시에 버그 수정은 release브랜치에서 수정
- QA 통과시, release를 master와 develop에 merge
- master 브랜치에 버전 태그 추가로 마무리
  
---

# 1. 티켓 처리
github-flow와의 차이점은 늘어난 branch 수
-> 기능 구현 전에 여러 티켓으로 작업을 나눈 후 처리해야 한다 (1 티켓 = 1 커밋)
- upstream/feature branch에서 작업 브랜치 생성
- 작업 브랜치에서 작업 수행
- 작업 브랜치에서 변경사항 commit
- commit을 2이상 합쳐햐 한다면 squash.
- 작업 브랜치를 feature 브랜치에 rebase
- 작업 브랜치를 origin에 push
- 작업 브랜치를 feature 브랜치에 merge하는 pull request 생성
- 동료 검사/리뷰 승인 후 pull request를 merge

---

# 2. develop 변경사항 feature에 가져오기
작업 중 기능 완료 전에 develop에서 기능이 추가, 그 기능이 필요한 경우 가져오기
- feature 브랜치에 develop 브랜치 merge
- develop의 변경사항이 merge된 feature를 push

---

# 3. 완료된 기능을 출시 버전에 포함시키기
feature 브랜치의 작업 완료시, develop에 merge 해야 한다.
- develop 브랜치에 feature브랜치를 merge
- feature를 merge한 develop 브랜치를 push
  
---

# 4. QA 시작
QA시작 전 release브랜치 행성, upstream에 push해서 공유
- release브랜치 생성
- release 브랜치 upstream에 push

---

 # 5. QA 중 버그 수정
버그 해결을 해야 출시 가능. 버그 처리도 티켓으로 관리-> 티켓처리와 유사
- release에 버그수정 브랜치 생성
- 버그 수정, 버그 수정 브랜치에 수정사항 커밋
- 버그 수정 브랜치를 origin에 push
- github에서 버그 수정 브랜치를 release 브랜치에 merge하는 pull request 생성
- 동료 리뷰 승인 후 pull request를 merge

---

# 6. 출시
release 브랜치를 master와 develop에 merge하고 master에서 버전테그를 달아둠
- release 브랜치 최신상태로 갱신
- release브랜치를 develop 브랜치에 merge
- develop 브랜치를 upstream에 push
- release 브랜치를 master에 merge
     > merge 전에 pull하고 진행
- 버전 태그 달기
- master 브랜치와 태그를 upstream에 push

---

# 용어설명

- push
  > local에서 remote로 올리는 것
- pull
  > remote의 데이터를 local로 가져와 병합
- fetch
  > remote의 데이터를 가져오기만 함(병합X)
  > 가져온 최신 커밋은 이름 없는 브랜치로 들어옴
  > fetch한 후 merge하면 pull 명령 실행과 결과 같아짐

---
# 용어설명
- merge
  > checkout 브랜치 기준으로 branch를 합병
  ![merge](https://backlog.com/git-tutorial/kr/img/post/stepup/capture_stepup1_4_5.png)
- rebase
  > checkout 브랜치가 제시된 branch로 변경이력들과 함께 들어감
  > branch의 위치들은 그대로이기 때문에 merge를 해줘야함
  ![rebase](https://backlog.com/git-tutorial/kr/img/post/stepup/capture_stepup1_4_8.png)


---

# 출처 / 참고
- https://techblog.woowahan.com/2553/
- https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html
