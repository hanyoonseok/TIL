# git clone --mirror
> 싸피에서 진행한 프로젝트를 내 깃허브로 반출할 때, 싸피랩의 커밋 내역을 그대로 유지한 채 레포지토리를 옮기기 위해선 `git clone --mirror`를 통해 가져오고 `git push --mirror`를 통해 푸쉬해야 한다. 그 과정에서 깃랩 레포지토리에서 덤프 파일 업로드로 인해 100M 이상의 파일을 커밋하고, 보유하고 있어서 깃허브에서 제한하는 문제가 발생했다.

### 100M 이상의 파일을 기존 레포지토리에서 핸들링한 적 없을 때
```
git clone --mirror ${기존 레포지토리 주소.git}
cd ${로컬에서 클론한 레포지토리의 폴더.git}
git remote set-url --push origin ${옮길 깃허브 레포지토리 주소}.git
git push --mirror
```

### 100M 이상의 파일을 커밋한 적 있거나, 아직 보유하고 있거나, 되돌리면 안될 때
- 우선 아래의 과정 거치기
```
협업 레포지토리를 포크하여 내 레포지토리로 가져오기
마스터 브랜치에서 100M 이상의 파일들 모두 제거하기
git clone --mirror ${기존 레포지토리 주소.git}
```
##### [Solution 1](https://velog.io/@alwaysryu13/gitlab-%EC%97%90%EC%84%9C-github-%EB%A0%88%ED%8D%BC%EC%A7%80%ED%86%A0%EB%A6%AC%EB%A5%BC-100MB%EC%9D%B4%EC%83%81-commit%EC%9D%84-%EC%9C%A0%EC%A7%80%ED%95%9C-%EC%83%81%ED%83%9C%EB%A1%9C-%EB%B3%B5%EC%82%AC%ED%95%98%EA%B8%B0)
- 이 방법은 다빈이가 해결한 방법이다.
- 나는 `fatal: bad revision 'lfs'`, `fatal: needed a single revision` 등의 에러를 마주하기도 하고, `remote rejected` 처럼 거부당하기도 하는 등의 이유로 해당 방법으로는 실패

[Solution 2(내가 해결한 방법)](https://coding-nurse.tistory.com/m/431)
- 화연이가 추천해준 방법이다.
- 커맨드 창에서 실행하지 않고 `git bash`로 실행했다는 점이 다르다
- 옮겨질 내 레포지토리의 디폴트 브랜치 명을 옮길 레포지토리의 디폴트 브랜치 명과 통일해주었다
- 옮길 레포지토리의 `branch protection`을 해제해주었다
- `fatal: needed a single revision`에러가 나기도 했는데, 그냥 무시하고 진행하니 결국 성공
