```javascript
// Array.prototype.sort
// 배열의 요소를 정렬 (기본 오름차순)
// 정렬 순서를 정의하는 비교함수를 인수로 전달 (반환값은 음수, 양수, 0) 
// 0보다 작으면 첫번째 인수를 우선하여 정렬, 0보다 크면 두번째 인수를 우선 정렬, 0 이면 정렬하지 않음

const score = [40, 30, 20, 50, 100];

console.log(score.sort((a, b) => a - b));

const todos = [
  {
    id: 4,
    content: 'Javascript',
  },
  {
    id: 1,
    content: 'HTML'
  },
  {
    id: 3,
    content: 'CSS'
  },
  {
    id: 1,
    content: 'HTML'
  }
];

console.log(todos);

function compare(id) {
  return (a, b) => (a[id] > b[id] ? 1 : (a[id] < b[id] ? -1 : 0));
}

console.log(todos.sort(compare('id')));

// Array.prototype.forEach
// for문을 대체할 수 있는 고차 함수
// 반환값은 undefined으로 따로 변수에 저장할 필요가없음

// forEach를 사용해 기존 배열의 요소들을 2배한값을 새롭게 선언된 배열에 저장

const numbers = [1, 3, 5, 6];
const newArr = [];

// 콜백 함수를 호출하면서 3개의 인수를 전달 (요소값, 인덱스, this)
numbers.forEach((value, index, array) => newArr.push(value * 2)); 
console.log(newArr);

// 원본을 변경 시키진 않지만 원한다면 변경 시킬수도 있음

numbers.forEach((value, index, array) => { array[index] = value * 2; });
console.log(numbers);

// 두번째 인수로는 this로 사용할 객체를 전달할수 있음

class Numbers {
  numberArray = [];

  triple(arr) {
    arr.forEach(function(item) {
      this.numberArray.push(item * 3)
    }, this) // 2번째 인수로 this 전달. 전달 하지 않을시 class내에서는 strict mode가 발동해서 undefined
  }
}

const num = new Numbers();
num.triple([1, 2, 3]);
console.log(num.numberArray);

// 화살표 함수를 사용하는 방법도 있음

class Numbers2 {
  numberArray = [];

  triple(arr) {
    arr.forEach(item => this.numberArray.push(item * 3)) // 화살표 함수의 this 는 상위 스코프를 참조 
  }
}

const num2 = new Numbers2();
num2.triple([1, 2, 3]);
console.log(num2.numberArray);

// Array.prototype.map
// forEach는 언제나 undefined를 반환하지만 map은 반환값들로 구성된 새로운 배열을 반환 

console.log(numbers); // [2, 6, 10, 12]
const mapArray = numbers.map((value, index, arr) => value / 2);
console.log(mapArray);

// Array.prototype.filter
// 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환

console.log(numbers); // [2, 6, 10, 12]
const filtered = numbers.filter((value, index, arr ) => value > 6 );
console.log(filtered);

// 특정 요소를 제거하기 위해 사용할수도 있음

class User {
  constructor(){
    this.users = [
      { id: 1, name: 'min'},
      { id: 2, name: 'won'}
    ]
  }

  findById(id) {
    return this.users.filter((user, index) => {
      return user.id === id 
    } )
  }

  removeById(id) {
    return this.users = this.users.filter((user, index) => user.id !== id) //전달받은 id와 일치하지 않는값만 유지
  }
}

const user = new User();
console.log(user.findById(1));
user.removeById(2);
console.log(user.users);  

// Array.prototype.reduce (원본 배열 변경 하지 않음 )
// 콜백 함수를 호출하여 하나의 결과값을 만들어 반환

// 배열에 있는 모든 요소의 값을 더하기

console.log(numbers); // [ 2, 6, 10, 12 ]
const sum = numbers.reduce((acc, val) => acc + val )
console.log(sum);

// 평균

const numbersAvg = [1, 2, 3];
const average = numbersAvg.reduce((acc, val, index, arr) => {
  const arrlen = arr.length;
  if (index === arrlen - 1) return (acc + val)/arrlen;
  else return acc + val;
}, 0)

console.log(average);

// 최대값

const numbersMax = [1,2,3,9,8];
const max = numbersMax.reduce((acc, val, index, arr) => {
  acc = acc > val ? acc : val;
  return acc; 
})
console.log(max);

// 요소의 중복 횟수
const numberRepeat = [1, 3, 4, 3, 3];
const repeated = numberRepeat.reduce((acc, val) => {
  acc[val] = (acc[val] || 0) + 1
  return acc
},{})
console.log(repeated);

// 중복 요소 제거 (이런건 filter 사용 권장)
// 모든 배열의 고차함수는 reduce로 구현가능하긴함

const deletedRepeats = numberRepeat.reduce((acc, val, index, array) => {
if (acc.includes(val) === false) {
  acc.push(val);
  }
  return acc;
}, []);

console.log(deletedRepeats);

// 객체의 특정 프로퍼티의 값을 확산해보기

const classmember = [
  {name: 'min', age: '28', score: 80},
  {name: 'won', age: '30', score: 95},
  {name: 'tom', age: '29', score: 100},
]

const avgScore = classmember.reduce((acc, val, i, arr) => {
  const len = arr.length;
  return i === len - 1 ? (acc + arr[i].score)/len : acc + arr[i].score;
}, 0)

console.log(Math.ceil(avgScore));

// Array.prototype.some
// 호출한 배열의 요소를 순회하며 인수로 전달된 콜뱀 함수를 호출 반환값이 단 한번이라도 참이면 true 아니면 false

console.log(classmember.some(val => val.score < 70)); //70미만 점수가 있는지 확인, 없으므로 false
console.log(classmember.some(val => val.score < 85)); //true

// Array.prototype.every
// 콜백함수의 반환값이 모두 참이면 true, 한개라도 false면 false

console.log(classmember.every(val => val.score > 70)); // 객체안 배열의 score 값이 모두 70이 넘기때문에 true
console.log(classmember.every(val => val.score < 99)) // score값이 100인 값이 있기 때문에 false

// Array.prototype.find
// 콜백함수의 반환값이 true인 첫번째 요소를 반환, 존재하지 않는다면 undefined 반환

const member = classmember.find(val => val.name === 'min'); //배열이 아닌 해당 요소의값(이 경우 객체)를 반환해 변수에 할당
console.log(member); 

// Array.prototype.findIndex
// 자신을 호출한 배열의 요소를 순회하면서 반환값이 true인 첫번째 요소의 인덱스를 반환

const memberIndex = classmember.findIndex(val => val.name === 'min'); 
console.log(memberIndex);

// Array.prototype.flatMap
// map 메서드와 flat 메서드를 순차적으로 실행, 1단계만 평탄화 할수 있음

const strings = ['hello', 'there']

console.log(strings.flatMap(x=> x.split('')));
console.log(strings.flatMap((str, index) => [index, [str, str.length]])); 
console.log(strings.map((str, index) => [index, [str, str.length]]).flat(2)); //평탄화 깊이를 지정하라면 map와 flat를 각각 호출

```