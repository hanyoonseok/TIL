# Git Flow

### Issue 생성
- 자신이 작업할 내용에 대한 이슈 생성
    - ex) [FE] 이슈 테스트 
- **생성한 이슈에 대한 `넘버`를 이후의 flow에서 사용**

### Branch 생성
- master : 배포 버전 작업물 
- develop : 개발 버전 작업물
- feature: 기능 개발 브랜치(issue 단위). 새로운 기능 개발시 브랜치명을 `feature/이슈번호`로 생성 후 해당 브랜치에서 개발
    - ex) 이슈번호가 3번일 때 브랜치 명은 `feature/3`

### Commit Message Convention에 따른 commit/push
- 정해진 커밋 메시지 컨벤션에 따라 메시지 작성
- 메시지 맨 뒤에 (#이슈번호) 기입
    - ex) `feat: 이슈 연습중 테스트 (#3)`

### PR Rule에 의거한 PR 요청
- feature/$ 에서 작업한 결과물은 바로 master나 develop으로 푸쉬하는게 아니라 develop 으로 PR을 보내야 함.
- PR명은 `[Be or Fe] 제목`으로 기입
- PR본문은 이슈번호로 기입
    - ex) PR명: `[Fe] 이슈 연습중` PR본문:`#3`

### PR 승인 후 develop 브랜치로 merge
