# 정규 표현식 RegExp

```javascript
  // 정규 표현식 

const target = 'Is this all there is';
const regexp = /is/i; // i -> 대소문자를 구별하지 않고 검색

regexp.test(target) // target 문자열이 /is/i 정규표현식에 부합하는지 확인; 부합함으로 true

// 생성자 함수를 통해 정규표현식 객체를 생성할 수도 있음
// new RegExp(pattern[, flags]); 

const exp = new RegExp(/is/i); 

// RegExp 메서드

// RegExp.prototype.exec
// exec 메서드는 인수로 전달받은 문자열에 대해 패턴을 검색하여 매칭 결과를 배열로 반환
// 없는 경우 null 반환

console.log(exp.exec(target)); // [ 'Is', index: 0, input: 'Is this all there is', groups: undefined ]

// RegExp.prototype.test
// 인수로 전달받은 문자열에 대해 패턴을 검색하고 매칭 결과를 불리언으로 반환

console.log(exp.test(target)); // true;

// String.prototype.match
// 문자열과 인수로 전달받은 표현식과의 매칭 결과를 배열로 반환
// exec는 첫번째 매칭 결과만 반환하지만 match는 모든 매칭 결과를 배열로 반환

const globalexp = /is/g;
console.log(target.match(globalexp)); 

// 플래그 (flag)
// 총 6개의 플래그가 존재
// i - ignore case, g - Global , m - multi line
// 선택적으로 순서와 상관없이 하나 이사으이 플래그를 동시에 설정 가능

// 패턴 
// 문자열 검색  - 위에 제시된 방법으로 진행

// 임의의 문자열 검색
// .가 임의의 문자열 검색

const random = /.../g;

// 반복 검색
// {m,n } 최소 m 번, 최대 n 번 반복되는 문자열을 의미

const repeatStr = 'A AA B BB Aa'
const repeat = /A{1,2}/g;

console.log(repeatStr.match(repeat));

// OR 검색
const orExp = /A|B/g;
console.log(repeatStr.match(orExp));
// 분해되지 않은 단어 검색은  /A+|B+/g;
// 범위를 지정하려면 [] 내에 - 사용 /[A-B]+/g;
// 대소문자 구별하지 않고 알파벳 검색 /[A-Za-z]+/g
// 숫자 검색 /[0-9,]+/g 또는 /[\d]+/g 
// 문자 /[\D,]+/g 
// 알파벳, 숫자 언더스코어 /w - [A-Za-z0-9_]

// NOT 검색
// [...] 내의 ^은 not의 의미를 가짐 /[^0-9]+/g

// 시작 위치로 검색
// [...] 밖의 ^은 문자열의 시작을 의미 - /^https/; https로 시작하는 문자열

// 마지막 위치로 검색
// $ 는 문자열의 마지막을 의미
const last = /com$/;

// 특정 단어로 시작하는지 검사
const url = 'https://example.com';
/^https?:\/\//.test(url);

// 특정 단어로 끝나는지 검사
const filename = 'index.html';
/html$/.test(filename);

// 숫자로만 이루어진 문자열인지 검사
const stringnum = '123456';
/^\d+$/.test(stringnum);

// 하나 이상의 공백으로 시작하는지 검사 /s -> 하나 이상의 공백으로 시작하는지 검사
const spaceword = ' Hi, there'
console.log(/^[/s]+/.test(spaceword));

// 아이디로 사용 가능한지 검사
const id = 'abc123';
console.log(/^[A-Za-z0-9]{4,10}$/.test(id));

// 메일 주소 형식에 맞는지 검사
// 문자열이 메일 주소 형식에 맞는지 검사

const email ='suhmingee@gmail.com';
/^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(email); // -> true

// 핸드폰 번호 형식에 맞는지 검사

const cell = '010-7888-9322';
/^\d{3}-\d{3,4}-\d{4}$/.test(cell);

// 특수 문자 포함 여부 검사

const special = 'abc#123';

// A-Za-z0-9 이외의 문자가 있는지 검사한다.
(/[^A-Za-z0-9]/gi).test(special); // -> true

```