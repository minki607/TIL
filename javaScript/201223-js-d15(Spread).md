# 스프레드 문법

- 하나로 뭉쳐있는 값들의 집할은 펼쳐 개별적인 값들의 목록으로 만듬

```javascript
  console.log(...[1,2,3]) // 1 2 3 ***값이아님
  console.log(...'Mingee'); // M I N G E E
```

- 스프레드 문법의 결과는 값이 아니기 때문에 변수에 할당 할수 없음
- 값의 목록으로 사용하는 문맥에서만 사용 가능
  - 함수 호출문의 인수 목록
  - 배열 리터럴의 요소 목록
  - 객체 리터럴의 프로퍼티 목록

## 함수 호출문의 인수 목록에서 사용

- 요소들의 집합인 배열을 펼쳐서 개별적인 값들의 목록을 전달해야 할때

```javascript
  const arr = [1, 2, 3];
  Math.max(arr); //여기서 max는 배열이아닌 인수를 받아야함으로 NaN이 나오므로 스프레드를 사용해줘야함
  
  Math.max(...arr) // 1,2,3 이 인수로 전달됨 따라서 max 값인 3 이 반환
```

- rest 파라미터 !== spread 문법 
    - rest는 인수들의 목록을 배열로 전달받음
    - spread는 배열과 같은 이터러블을 펼쳐서 개별적인 값들의 목록을 만드는 반대개념

## 배열 리터럴 내부에서 사용하는 경우

- 원래 es5에서는 2개의 배열을 합치고 싶을때는 `concat`을 사용해야 했지만 스프레드 문법으로 이를 대체할수 있음

```javascript
  const array = [...[1,2], ...[3,4,5]] // [1,2,3,4,5]
```
- 배열 중간에 `splice`를 사용해 다른 배열을 추가할때도 유용함
```javascript
// ES6
const arr1 = ['hi', 'there'];
const arr2 = ['wat', 'up'];

arr1.splice(1, 0, ...arr2);
console.log(arr1); // ['hi', 'there', 'wat', 'up']

// 얕은 복사도 할수 있음
const original = [1,2,3];
const copy = [...original]

console.log(copy) // [1,2,3

```


## 객체 리터럴 내부에서 사용하는 경우

- TC39 4단계에 제안되어 있는 스프레드 프로퍼티를 사용하면 객체 리터럴의 프로퍼티 목록에서도 사용가능
- 
```javascript
//Object.assign 대신에 spread문법을 사용해 간단히 추가 가능
const obj = { x: 1, y: 2 };
const copy = { ...obj };

const added = { ...{ x: 1, y: 2 }, z: 0 };
// {x:1, y:2, z:0}

const user = {
  name: 'Lee',
  family: {
    member: ['mom', 'dad', 'bro']
  }
};

const { family: { member } } = user;
console.log(member);

```



