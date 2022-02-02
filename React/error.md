# axios 에러 처리
- `Rubminds` 프로젝트 진행 도중 axios요청을 보냈을 때 에러를 처리해야 할 일이 있었음.
```jsx
function evaluateTeamMembersAPI(data) {
  return axios.post(`/team/${data.teamId}`, data.content, {
    headers: {
      Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
    },
  });
}
function* evaluateTeamMembers(action) {
  const result = yield call(evaluateTeamMembersAPI, action.data);
  console.log(result);
  try {
    yield put({
      type: EVALUATE_TEAM_MEMBERS_SUCCESS,
      data: result,
    });
  } catch (err) {
    console.log(err);
    yield put({
      type: EVALUATE_TEAM_MEMBERS_ERROR,
      error: err,
    });
  }
}
```
- 위와 같이 saga를 통해 위와 같이 작성했는데, 서버로 api 요청 중 에러가 발생하면 `const result = yield call(evaluateTeamMembersAPI, action.data);`라인에서 에러가 발생하기 때문에 그 아래에 있는 `try catch`에서 걸리지 않음.
- catch문 안에서 err를 찍어봐도 걸리지 않음
- 찾아보니 axois 요청에서 나온 에러는 `error.response`에 저장됨. 단순히 `error`를 검색해도 나오지 않음

```jsx
function addTeamUserAPI(data) {
  return axios.post(`/team/${data.teamId}/user/${data.userId}`, null, {
    headers: {
      Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
    },
  });
}
function* addTeamUser(action) {
  console.log(action.data);
  let result;
  try {
    result = yield call(addTeamUserAPI, action.data);
    try {
      yield put({
        type: ADD_TEAM_USER_SUCCESS,
        data: result,
      });
      alert('수락되었습니다');
    } catch (err) {
      yield put({
        type: ADD_TEAM_USER_ERROR,
        error: err,
      });
    }
  } catch (err) {
    alert(err.response.data.error.info);
  }
}
```
- 에러가 발생할 수 있는 axios 요청이 들어간 라인을 `try`문 안에 넣어주었고, 이 블럭 안에서 성공했을 경우 try-catch로 연결해주었음. 
- 에러가 발생할 경우 `err.response.data`를 통해서 서버로부터 온 에러를 캐치할 수 있고, depth를 더 깊이 접근하여 서버에서 보낸 메시지까지 확인하여 띄울 수 있음
