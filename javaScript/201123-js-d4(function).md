# 함수 (function)

- 수학에서 함수란 입력을 받아 출력을 내보내는 과정
- 프로그래밍에서 함수는 이 과정을 문으로 구현하고 코드블록으로 감싸 하나의 실행단위를 만드는 개념.

![함수 구성요소](https://poiemaweb.com/assets/fs-images/12-2.png)

매개변수: 함수 내부로 입력을 전달받는 변수
인수: 함수 호출시 입력받는 값
반환값: 함수 블록의 결과를 출력

### 함수를 쓰는 이유

- 필요시 여러번 호출 가능 ( 재사용성 )
- 중복 코드 제거
- 유지 보수 ( 코드 수정 )
- 코드의 가독성 향상
- 실수를 줄여 코드의 신뢰성을 높힘

## 함수 리터럴 

- 함수 또한 객체 타입의 값이기 때문에 객체를 객체 리트럴로 생성가능하듯이 함수도 리트럴로 생성할수 있음.

함수 리터럴의 구성요소 

<b>키워드</b>

`function`

<b>함수 이름</b>
- 식별자 네이밍을 규칙을 준수해야함
- 생략할수도 있음. 이름이 있는 함수 = 기명 함수,  없는 함수 = 익명 함수. 

<b>매개변수 목록</b>

- 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분
- 순서대로 할당
- 식별자 네이밍 규칙을 준수해야함 

<b>함수 몸체<b>

- 함수가 호출되었을때 일괄적으로 실행될 문들을 하나의 실행단위로 정의한 코드 블록

## 함수 정의 

함수 정의 방법

- 함수 선언문

```javascript
function add(x, y) {
  return x + y;
}
```
- 함수 표현식
```javascript 
var add = function (x, y) {
  return x + y;
};
```
- Function 생성자 함수
```javascript
var add = new Function('x', 'y', 'return x + y'); 
```
- 화살표 함수

```javascript
var add = (x, y) => x + y;
```

## 함수 선언문

- 함수 선언문은 표현식이 아닌 문이기 때문에 변수에 할당할 수 없지만 아래 예제를 살펴보면 할당이 된것 처럼 보임. 

```javascript
  var add = function add(x, y) {
    return x+y;
  }
```

이는 사실 함수 선언문이 아니고 자바스크립트 엔진이 문맥상 함수 리터럴로 해석하기 때문임.

- 기명 함수 리터럴은 단독으로 사용하면 -> 함수 선언문
- 피연산자로 사용하면 -> 함수 리터럴 표현식

함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가르키는 식별자로 호출.

따라서,

자바스크립트는 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성한뒤 객체를 할당함.

## 함수 표현식

일급 객체 - 값의 성질을 갖는 객체 

함수는 일급 객체이므로 함수 리터럴로 평가된 함수 객체를 변수에 할당하는게 가능.

이러한 함수 정의 방식을 <b>함수 표현식</b>이라 함.

## 함수 호이스팅

함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출 가능 (호이스팅)
함수표현식으로 정의한 함수는 함수 표현식 이전에 호출 불가능

함수 선언문으로 정의된 함수에서의 호이스팅은 변수 호이스팅과는 달리 undefined가 할당되지 않고 바로 호출할수 있음.

함수 표현식을 사용하면 함수 호이스팅이 발생하지 않고 변수 호이스팅이 발생함.

```javascript
 //sub 이라는 변수가 런타임 이전에 호이스팅되고 undefined로 초기화 됨. 나머지 함수 표현식의 함수리터럴은 런타임에 할당됨.
var sub = function (x, y) { 
  return x+y;
}
```
* 함수 호출 이전에 함수를 선언하는게 논리적이기 때문에 함수 선언문 대신 함수 표현식을 사용해 가독성을 높히는걸 권장.

### Function 생성자 함수

`var add = new Function()`<br>
Function 생성자 함수를 사용해 함수를 생성하는 방식도 있지만 일반적이지 않고 함수 선언문이나 함수 표현식으로 생성된 함수와 다르게 동작하기 때문에 추천하지 않음.

### 화살표 함수.

`const add = (x, y) => x + y;` <br>
좀 더 간략한 방법으로 함수를 선언할수 있게 es6에 추가된 방법. 그냥 표현만 더 간략한게 아니라 내부동작 또한 간략화 되있기 때문에 사용시 주의가 필요.


## 함수 호출

![함수호출구성](https://poiemaweb.com/assets/fs-images/12-9.png)

매개 변수 
- 함수 내부에서만 참조가능 (스코프는 함수 내부)
- 개수와 인수의 개수가 일치하는지 체크 하지 않음.
- 인수가 할당되지 않는 매기변수의 값은 undefined
- 매개 변수보다 인수가 많은 경우 초과된 인수는 무시, arguments 객체의 프로퍼티로 보관.
- 최대 개수는 제한하지 않지만 이상적인 함수는 한가지 일만 해야 하며 가급적 작게 만들어야하기 때문에 최대한 매개변수의 수를 줄여주는게 좋음.

## 반환문 

함수 내부 return 키워드와 표현식으로 이러우전 반환문을 외부로 반환할수 있음.

반환문은 
  - 함수의 실행을 중단하고 함수 몸체를 빠져나감 ( return 이후에 코드는 실행되지 않음 )
  - return 키워드 뒤에 오는 표현식을 평가해 반환
  - 표현식을 명시적으로 지정하지 않으면 undefined가 반환.

## 외부 상태의 변경

- 원시 타입인수는 값 자체가 복사되어 매개변수에 전달되기 때문에 함수 몸체에서 값을 변경해도 원본은 변경되지 않음. 즉, 외부에서 전달받은 값이 함수 몸체 내부에서 변경되는 부수효과가 없음.

- 객체 타입의 경우 참조 값이 복사되어 전달되기 때문에 몸체에서 참조값을 통해 객체를 변경하면 원본이 변경됨. 즉, 부수효과가 있음. 해결방안으로는 객체를 불변 객체로 만들어 사용하는것. (깊은 복사를 통해 새로운 객체를 생성하고 재할당을 통해 교체).

- 외부 상태를 변경하지 않고 외부 상태에 의존하지 않는 함수를 <b>순수함수<b>라고함.

## 함수의 형태

### 즉시 실행 함수
- 함수 정의와 동시에 즉시 호출되는 함수
- 한번만 실행되며 다시 호출할수 없음.
- 그룹 연산자로 감싸줘야함 ( 함수 리터럴을 평가해서 함수 객체를 생성하기 위해

### 재귀 함수 (Recursive Function)

- 함수가 자기 자신을 호출하는 행위.
- 반복되는 처리를 위해 사용.
- 탈출 조건을 만들어주지 않으면 무한으로 호출하기 때문에 stack overflow 현상이 일어남
- 일반적인 경우 반복문을 이용하는게 가독성면에서는 더 좋을수 있으나 재귀함수를 이용해 직관적으로 이해하기 더 쉬운 코드를 짤수 있다면 사용하길 권장.

### 중첩 함수 (Nested Function)

- 함수 내부에 정의된 함수
- 외부함수 - 중첩 함수를 포함하고 있는 외부에 있는 함수, 내부함수 - 함수 안에 있는 함수 
- 내부함수는 외부에 함수에 정의되어 있는 변수를 참조할수 있음

### 콜백 함수 (Callback Function)

- 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수

고차 함수 - 함수를 인자로 받거나, 함수를 반환함으로써 작동하는 함수.
콜백 함수는 고차함수에 전달되어 헬퍼 함수의 역활을 함.  

콜백함수는 고차 함수에 의해 호출되고 필요에 따라 콜백 함수에 인수를 전달 할수 있음