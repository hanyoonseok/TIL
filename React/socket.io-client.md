# Socket.io-client
> socket.io를 통해 서버와 소켓통신을 하기 위해서 필요한 클라이언트 측 모듈  
> `npm install socket.io-client`

```
import io from 'socket.io-client';
const socket = io(${백엔드주소});
```
- 서버에서 받을 이벤트는 `on`, 서버로 보낼 이벤트는 `emit`으로 사용.
```
socket.on('connection',(){
  socket.emit('message',{name, message});
})
```
