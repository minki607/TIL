# 디스트럭처링 할당

- 구조화된 배열과 같은 이트러블 또는 객체를 비구조화하여 1개 이상의 변수에 개별적으로 할당

```javascript
// ES5
var arr = [1, 2, 3];

var one   = arr[0];
var two   = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3

//ES6

const [one, two, three] = arr;
console.log(two) //2
```

- 디스트럭처링 기준은 배열의 인덱스. 즉 순서대로 할당 됨.
- 요소가 반드시 일치할 필요하는 없음 

```javascript
const [a, b] = [1]; // a = 1 b = undefined
console.log(c, d); //1, undefined

// 디스트럭처링 할당을 위한 변수에 기본값을 설정할수도 있음
const [a, b, c = 3] = [1, 2]; // a = 1 b = 1 c = 3
```

- 배열 디스트럭처링 할당을 위한 변수에 Rest 파라미터와 유사하게 Rest 요소(Rest element) 를 사용할수 있음
Rest 요소는 Rest 파라미터와 마찬가지로 반드시 마지막에 위치해야함

```javascript
const [first, ...rest] = [1, 2, 3, 4, 5];
console.log(first, rest); // 1 [ 2, 3, 4, 5 ] 
console.log(first) //1
console.log(rest) // [ 2, 3, 4, 5 ]
```

## 객체 디스트럭처링 할당

- 객체의 각 프로퍼티를 객체로부터 디스트럭처링하여 할당하기 위해선 프로퍼티 키를 사용

```javascript
var user = { firstName: 'Min Gee', lastName: 'Suh' };

const {firstName, lstName } = user; // 순서는 상관없고 선언된 변수 프로퍼티 키와 일치해야함

// const { lastName: lastName, firstName: firstName } = user;
```

- 필요한 프로퍼티 값만 추출하여 변수에 할당하고 싶을때 유용
- 인수로 전달받는 함수의 매개변수에도 사용할수 있음

```javascript
function printTodo({content, completed}) {
  console.log(`할일 ${content}은 ${completed ? '완료' : '비완료'} 상태입니다.`);
}

printTodo({ id: 1, content: 'HTML', completed: true });
```

중첩 객체
```javascript

const user = {
  name: 'Lee',
  family: {
    member: ['mom', 'dad', 'bro'],
    total: member.length
  }
};

// address 프로퍼티 키로 객체를 추출하고 이 객체의 city 프로퍼티 키로 값을 추출한다.
const { address: { city } } = user;
console.log(city); // 'Seoul'
```

