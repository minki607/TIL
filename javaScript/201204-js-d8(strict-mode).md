# Strict


## strict mode의 적용

- es5부터 strict mode가 추가됨.
- 오류를 발생시킬 가능성이 높고 엔진의 최적화 작업에 문제를 일으킬수 있는 코드에 대해 에러를 발생 시킴
- 코드 몸체의 선두에 `use strict;`를 추가함

```javascript
'use strict';

function foo() {
  x = 10;
}
foo();

//전역객체 x 프로퍼티를 동적으로 생성하지 않고 reference error를 발생시킴
```


<b>암묵적 전역</b>

- 선언하지 않은 변수를 참조하면 ReferenceError가 발생

<b>변수, 함수, 매개변수의 삭제</b>

- delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxErro

<b>매개변수 이름의 중복</b>

- 중복된 매개변수 이름을 사용하면 SyntaxError가 발생

<b>with 문의 사용</b>

- with 문을 사용하면 SyntaxError가 발생.

<b> 일반 함수의 this </b>

- strict mode에서 함수를 일반 함수서 호출시 undefined가 바인딩.

<b> arguments 객체 </b>

- 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다. 
