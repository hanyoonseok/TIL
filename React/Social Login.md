# 카카오 로그인
<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCe4MA%2Fbtq4wuv8wfO%2FDPsWToxRqBTcRl4fQjeDak%2Fimg.png">

- 프론트가 해주어야 할 일은 카카오로부터 인가코드를 받고, 받은 인가코드를 백엔드 서버로 넘겨주어야 함.
- 그 후 서버로부터 가공된 토큰을 저장 후 사용자를 redirect 해주면 됨.

### 1. 인가 코드 받기 설정
- `https://developers.kakao.com/console/app` 접속 후 `내 애플리케이션`에서 애플리케이션 추가
- 애플리케이션의 REST API 키 복사
- `카카오 로그인` 탭으로 이동 후 활성화 체크하고 Redirect URI 설정.(개발 주소와 배포주소 모두 설정)
- `플랫폼` 탭으로 이동 후 웹 플랫폼 등록(개발시 localhost:3000, 배포시 배포링크) 
    
### 2. 인가 코드 받기
- a 태그의 href에 `https://kauth.kakao.com/oauth/authorize?client_id=${CLIENT_ID}&redirect_uri=${REDIRECT_URI}&response_type=code` 링크의 `CLIENT_ID`자리에 복사해뒀던 `REST API키`를, `REDIRECT_URI` 자리에 설정했던 REDIRECT 주소를 넣음.
- 해당 링크 열었을 때 `동의하고 계속하기` 버튼을 눌렀을 때 나오는 redirect_uri 주소창 뒤에 파라미터로 나오는 `?code=@`가 인가코드임.
- redirect 될 화면에서 `let code = new URL(window.location.href).searchParams.get("code") 를 통해 인가 코드만 따옴

### 3. 백엔드로 전송 후 redirect
- axios 통신으로 백엔드에 인가 코드를 전송 후(이때 인가 코드는 쿼리 스트링으로 넘겨야 함), 백엔드로부터 토큰 받기.
    - `axios.get('서버주소?code=${code}')`
- 토큰 저장 후 화면 전환
 
[참고](https://data-jj.tistory.com/53)
