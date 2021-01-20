# 프로미스 (promise)

비동기 처리를 하기위해 ES6에 도입된 패턴으로 콜백 함수를 사용하는 기존의 방식보다 가독성이 뛰어남.

## 프로미스 생성 

```javascript
  const promise = new Promise((resolve, reject) => { /*코드 내부. 비동기 처리 성공시 resolve 함수에 인수로 전달하면서 호출 실패시 reject 함수에 인수로 전달*/})
```

프로미스는 비동기 처리 진행 상태 정보를 가지는데 resolve (첫번째 인수)가 호출되었을때와 reject (두번째 인수)가 호출되었을때의 상태값이 다름.

- pending (비동기 처리 수행하지 않은 상태)
- settled (치리 완료)
  - fulfilled (비동기 처리 성공) - resolve 함수 호출
  - rejected (비동기 처리 실패)  - reject 함수 호출

## 프로미스 후속 처리 메서드

- then 
```javascript
const promise = new Promise((resolve, reject)=> {
  if (/*비동기 성공 조건*/) {
    setTimeout(()=>{
        resolve("resolved");
      }, 3000);
  } else {
    reject(new Error("rejected"))
  }
});

// 비동기 처리가 성공했을때는 첫번째 콜백함수를 , 실패했으면 두번째 콜백함수를 호출
promise.then(value => console.log(value), err => console.error(err));
```
**만약 then이 여러개 있다면 다른 콜백함수에서 발생한 에러를 캐치하지 못할수도 있으니 가독성이 안좋은 then의 두번째 인수를 사용하는것보단 catch를 쓰는걸 권장

- catch
프로미스가 rejected 상태인 경우만 호출

```javascript 
const promise = new Promise((resolve, reject)=>{
  setTimeout(()=>{
    reject(new Error('rejected'));
  }, 3000);
});
promise.then(result => console.log(result)).catch(error => console.error(error));
// 3초 후에 rejected 에러가 출력
```
- finally

상태와 상관없이 무조건 한번 처리할 내용이 있을 경우 사용

```javascript
  new Promise(() => {}).finally(() => console.log('this will be triggered at least once'))
```

## 프로미스 정적 메서드

```javascript
const resolvedPromise = Promise.resolve([1,2,3]);
resolvedPromise.then(console.log);

const rejectedPromise = Promise.resolve(['hello']);
rejectedPromise.then(v => console.log(v), e => console.error(e));

const requestData1 = () => new Promise(resolve => setTimeout(() => resolve(1), 3000));


const requestData2 = () => new Promise(resolve => setTimeout(() => resolve(2), 1500));


const requestData3 = () => new Promise((resolve, reject) => setTimeout(() => reject(new Error('custom error')), 1000));


Promise.all([requestData1(), requestData2(), requestData3()])
.then(value => console.log(value))
.catch(console.error)

// 깃허브 아이디로 이름 찾기 Promise.all
const fetchGithubId = username => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', `https://api.github.com/users/${username}`);
    xhr.send();
    xhr.onload = () => {
      if (xhr.status === 200) resolve(JSON.parse(xhr.response));
      else reject(new Error(xhr.status));
    }
  })  
}

const githubID = ['minki607', 'HaJunRyu', 'yg-0103'];

Promise.all(githubID.map( id => fetchGithubId(id)))
.then(users => users.forEach(user => console.log(user.name)))
.catch(console.error);


// Promise.race
// 가장 빠르게 resolve 또는 reject 된 프로미스를 반환
Promise.race([requestData1(), requestData2(), requestData3()])
.then(console.log)
.catch(console.error);

// Promise.allSettled 전달된 프로미스가 모두 settled (resolved, rejected) 되었을때 처리결과를 반환

Promise.allSettled([requestData1(), requestData2(), requestData3()])
.then(console.log)
.catch(console.error);

// [
//   { status: 'fulfilled', value: 1 },
//   { status: 'fulfilled', value: 2 },
//   {
//     status: 'rejected',
//     reason: Error: custom error
//         at Timeout._onTimeout (/Users/min/dev/json-server-exam/app.js:13:85)
//         at listOnTimeout (internal/timers.js:549:17)
//         at processTimers (internal/timers.js:492:7)
//   }
// ]

// fetch - HTTP 응답을 나타내는 response 객체를 래핑한 프로미스 객체를 반환 (WEB API)


fetch('https://pokeapi.co/api/v2/pokemon/1')
.then(response => response.json())
.then(json => console.log(json.name))
.catch(console.error);

const request = {
  get(url) {
    return fetch(url)
  }
}

request.get('https://pokeapi.co/api/v2/pokemon')
.then(pokemons => pokemons.json())
.then(jsonpoke => jsonpoke.results.map(pokemon => console.log(pokemon.name)))
```
