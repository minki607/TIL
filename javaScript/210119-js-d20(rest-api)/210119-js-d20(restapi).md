# REST API

HTTP의 장점을 최대한 활용할수 있도록 설계한 아키텍쳐.

- 자원 (Resource) 
- 행위 (Verb)
- 표현 (Representation)

설계 원칙

- URI는 리소스를 표현해야함 (get, post 처럼 행위에 대한 표현을 쓰지말것)
`/get/todos/1` x <br>
`/todos/1` o
- 행위는 HTTP 요청 메서드로 표현
`GET /todos/1` <br>
`DELETE /todos/1`

```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');
xhr.send(); // HTTP 요청 전송
xhr.onload = () => {
  if (xhr.status === 200) {
    console.log(JSON.parse(xhr.response));
  } else {
    console.error('Error', xhr.status, xhr.statusText);
  }
};
```

<b>
GET, POST, PUT, PATCH, DELETE 요청 예제는 json-server-exam 폴더 참고!
</b>