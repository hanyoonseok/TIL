# immer
> 불변성 유지를 쉽게 도와주는 툴
### 설치
`npm install immer`

### 적용
- `immer` 적용 전
- 불변성 유지를 위해 `...` 사용이 많고, 가시성이 매우 떨어짐
```jsx
//reducers/post.js
case ADD_COMMENT_SUCCESS: {
  const postIndex = state.mainPosts.findIndex(
   v => v.id === action.data.postId
  )
  const post = { ...state.mainPosts[postIndex] }
  post.Comments = [dummyComment(action.data.content), ...post.Comments]
  const mainPosts = [...state.mainPosts]
  mainPosts[postIndex] = post
  return {
     ...state,
     mainPosts,
     addCommentLoading: false,
     addCommentDone: true,
  }
}
```
- `immer` 적용 후
```jsx
case ADD_COMMENT_SUCCESS: {
  const post = draft.mainPosts.find((v)=>v.id === action.data.postId);
  post.Comments.unshift(dummyComment(action.data.content)); //배열의 불변성을 유지하면서 넣어줌
  draft.addCommentLoading=false;
  draft.addCommentDome = true;
  break;
}
```
