# Promise

## Promise에 대해서 알고 있나요?

프로미스는 자바스크립트 비동기 처리에 사용되는 객체입니다. 일반적으로 `fetch` 함수를 통해 데이터를 받아올 때 사용됩니다.

## Promise는 왜 쓰는 건가요?

서버에 데이터를 요청하고 데이터를 받아오는 과정에서 데이터를 다 받아온 것처럼 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜹니다.
이를 해결하기 위해 나온 것이 Promise입니다.

## 비동기 처리가 뭔가요?

- 동기식(Synchronous): 작업이 끝날 때까지 다른 작업을 시작하지 않고 기다리는 방식
- 비동기식(Asynchronous): 작업의 완료 여부와 상관없이 새로운 작업을 시작하는 방식

## 자바스크립트에서는 어떤 비동기 처리 방식이 있나요?

- `Callback` 함수 이용
- `Promise`
- `async/await`

## 어떤 경우에 비동기 처리를 해야할까요?

- 사용자 이벤트 처리 시
- 네트워크 응답 처리 시
- 파일을 읽고 쓰는 등의 파일 시스템 작업 시
- 의도적으로 시간 지연을 사용할 때

## 참고

[자바스크립트 Promise 쉽게 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)
[[Javascript] 비동기, Promise, async, await 확실하게 이해하기](https://springfall.cc/article/2022-11/easy-promise-async-await)