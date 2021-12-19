# 알아두면 좋은 git 사용법
### git clone
> 레포지토리를 새롭게 복제하여 가져오기 위함. git clone으로 생성하면 `origin` 이라는 리모트 저장소가 자동으로 등록.
```
git clone $url
```

### git initialize
> 프로젝트에 깃 저장소 구성을 위한 .git 추가하기 위함.
```
git init
```

### git status
> 저장소 내 파일들의 상태, 사용중인 브랜치 출력
```
git status
```

### 리모트 저장소
- 리모트 저장소 확인
```
git remote //현재 사용중인 저장소 이름 출력
git remote -v
```
`-v` 옵션으로 저장소의 단축 이름과 url 출력
- 리모트 저장소 추가
```
git remote add origin(저장소명) url 
```

### git add
> 작업 디렉토리 상의 변경내용을 staging area에 추가
```
git add . //변경사항 모두 추가
```
### git pull
```
git pull origin(원격저장소명) dev(브랜치명) //브랜치 내용 
```

### git commit
> staging area에 있는 현재까지의 변경사항을 확정.
```
git commit -m "커밋메시지"
git commit -a "커밋메시지" // -a 옵션으로 add까지 한번에 진행 가능
```

### git push
> 원격 저장소에 코드 변경분을 업로드
```
git push 저장소명 브랜치명
```
`-u`옵션을 통해 최초 한 번만 저장소명과 브랜치명을 입력하면 이후로는 `git push`만 입력해도 자동으로 푸쉬 가능.  
```
git push -u 저장소명 브랜치명

//이후에 push 할 때는
git push
```

### git branch
- 브랜치 생성
```
git branch 브랜치명
```
- 브랜치 출력
```
git branch
git branch -a // 원격 브랜치까지 모든 브랜치 보여줌
```
- 브랜치 변경
```
git checkout 브랜치명
git checkout -t origin(원격저장소명)/master(브랜치명) // 원격 저장소의 branch로 변경
```
> 새로 clone한 프로젝트에서 브랜치를 새로 만들고, 해당 브랜치로 checkout -t 한 후, git pull master 하면 새로운 브랜치에 그대로 가져올 수 있음.

### git stash
> 아직 마무리하지 않은 작업을 스택에 잠시 저장.
```
git stash
```
- stash 목록 확인
```
git stash list
```
- 했던 작업 다시 가져오기
```
git stash apply stash@{}
git stash apply --index //--index 까지 넣어야 staged 상태까지 복원
```
- stash 제거
```
git stash drop //가장 최근의 stash 제거
```
`apply`는 단순히 stash를 적용하는 것일 뿐, 여전히 스택에는 남아있음.
```
git stash pop // apply + drop
```

**feat브랜치에서 작업할 내용을 master에서 작업해버렸을 때**

```
//master branch에서
git stash push
git checkout [이동할 브랜치]
git stash pop
```

### 커밋 취소
> 아직 푸쉬하지 않은 커밋을 취소하거나, 이전 커밋상태로 되돌아가기
- 변경내역은 유지, 커밋만 취소 
```jsx
git log //커밋한 로그 확인
git reset --soft [로그에서 확인한 돌아갈 커밋아이디] //현재까지 변경내역은 그대로, 커밋만 
git pull origin 브랜치
```
- 아예 이전 커밋상태로 되돌아가기(현재까지 변경내역 삭제)
```jsx
git log
git reset --hard [로그에서 확인한 돌아갈 커밋아이디]
```
- git add 취소
```jsx
git reset HEAD [파일명] //파일명 안 붙이면 모든 add 취소
```

[git 실습해보기](https://learngitbranching.js.org/?locale=ko)
