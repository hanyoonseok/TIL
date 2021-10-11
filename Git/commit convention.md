# GIT COMMIT CONVENTION
> [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/) 를 참고하여 작성하는 git commit convention

### Structure
```
<TITLE>

<BODY>

<FOOTER>
```

### TITLE
- <타입>: <제목> 형식 (최대 50자)
- 제목 끝에 특수문자 금지(. , ! ?)
- `제목`은 동사 원형으로 시작
```
feat: add login component
```

타입 | 설명
--|--
feat|새로운 내용 추가
fix|버그 수정
docs|문서수정
test|테스트 코드 추가
refactor|코드 리팩토링
comment|새로운 주석 추가 및 변경
style|코드 의미에 영향을 주지 않는 변경사항(css, 세미콜론 누락)
chore|빌드 부분 혹은 패키지 매니저 수정사항
rename|파일 혹은 폴더명을 수정, 옮기는 작업
remove|파일 혹은 폴더 제거

### BODY
- 72자 이내로 작성
- 내용을 어떻게 변경했는지, 무엇을 변경했는지, 왜 변경했는지 작성
```
component 폴더에 login.tsx 로그인 컴포넌트 추가 작성
app.tsx에서 라우팅 완료
```

### FOOTER
- <타입>: <#이슈번호> 형식 
```
Resolves: #123
Ref: #456
Related to: #46, #34
```
타입 | 설명
--|--
Fixes|이슈 수정중(아직 해결하지 않은 경우)
Resolves|이슈 해결
Ref|참고할 이슈 있을 때
Related to|해당 커밋에 관련된 이슈번호(아직 미해결)

### 전체 예시
```
feat: add login component

component 폴더에 login.tsx 로그인 컴포넌트 추가 작성
app.tsx에서 라우팅 완료

Resolves: #123
Ref: #456
Related to: #46, #34
```

### 커밋 템플릿
> git commit 메시지를 정해진 양식에 따라 작성할 수 있게 도와줌  
1. 커밋 메시지 템플릿 적용할 git 프로젝트에 진입 후 `.gitmessage.txt`파일 생성
2. 아래의 양식을 파일에 추가
```
# TITLE
# <타입>: <제목> (최대 50자)
# 제목을 아랫줄에 작성, 제목 끝에 특수문자 금지(. , ! ?), 제목은 동사 원형으로 시작
# ex) feat: add login component

################
# BODY
# 본문(추가 설명)을 아랫줄에 작성 (최대 72자)
# 내용을 어떻게 변경했는지, 무엇을 변경했는지, 왜 변경했는지 기술

################
# FOOTER
# 꼬릿말(footer)을 아랫줄에 작성 (관련된 이슈 번호 등 추가)
# <타입>: <#이슈번호> 형식

################
# TITLE 타입
# feat : 새로운 기능 추가
# fix : 버그 수정
# docs : 문서 수정
# test : 테스트 코드 추가
# refactor : 코드 리팩토링
# comment : 새로운 주석 추가 및 변경
# style : 코드 의미에 영향을 주지 않는 변경사항(css, 세미콜론 누락)
# chore : 빌드 부분 혹은 패키지 매니저 수정사항
# rename : 파일 혹은 폴더명을 수정 or 옮기는 작업만 한 경우
# remove : 파일 혹은 폴더 제거만 한 경우
################
# FOOTER 타입
# Fixes : 이슈 수정중(아직 해결하지 않은 경우)
# Resolves : 이슈 해결했을 때
# Ref : 참고할 이슈 있을 때
# Related to: 해당 커밋에 관련된 이슈번호 (아직 해결하지 않은 경우)
# ex) Resolves:#123 Ref:#456 Related to :#48, #5
################
```
3. `git config --global commit.template .gitmessage.txt` 명령어 입력
4. 커밋시 `git commit`으로 실행
5. `vi 에디터` 나오면 `i`키를 눌러 수정 시작, 다 작성 후 `:wq!`입력 후 엔터
