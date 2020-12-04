# 프로토타입(Prototype)

- 상속을 통해 불필요한 중복을 제거하기 위해 사용됨 (객체 간 상속)
- 프로토타입을 상속받은 하위 객체는 상위객체의 프로퍼티를 자신의 프로퍼티처럼 사용가능

모든 객체는 `[[Prototype]]`라는 내부슬롯을 가지며, 저장되는 포로토타입은 객체 생성 방식에 의해 결정됨

- 객체 리터럴 - `Object.prototype`
- 생성자 함수 - `prototype` 프로퍼티에 바인딩되어 있는 객체

`[[Prototype]]` 내부 슬롯에에 직접 접근할 순 없지만 `__proto__` 접근자 프로퍼티를 통해 자신의 프로토타입에 간접적으로 접근할수 있음

프로토타입은 `constructor` 프로퍼티로 생성자 함수에 접근할수 있고, 생성자 함수는 prototype 프로퍼티를 통해 프로토타입에 접근할수 있음.

![prototype binding](https://poiemaweb.com/assets/fs-images/19-3.png)

모든 객체는 `__proto__` 접근자 프로퍼티를 통해 프로토타입 (`[[Prototype]]`) 내부 슬롯에 간접적으로 접근 가능

- `__proto__ 는 접근자 프로퍼티다`
  - getter/setter 접근자 함수를 통해 내부 슬롯의 값을 불러오거나 할당함.
- `__proto__ 접근자 프로퍼티는 상속을 통해 사용돤다`
  - `__proto__`는 `Object.prototype`의 프로퍼티이므로 모든 객체는 Object의 하위 요소이기 때문에 상속을 통해 인스턴스 객체에도 사용할수 있는것
- `__proto__ 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유`
  - 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해
  - 아무런 체크없이 무조건적으로 포로토타입을 교체할수 있다면 서로가 서로의 프로토타입이 되서 순환 참조를 할 수 있기 때문에 `__proto__` 를 사용해 이를 방지
- `__proto__ 접근자 프로퍼티를 코드 내에서 직접 사용하는것은 권장하지 않음` 
  - es6에서 표준으로 채택되었지만 모든 코드가 __proto__접근자 프로퍼티를 사용할 수 있는건 아님.
    예를들어 `const obj = Object.create(null);` 에서 obj 는 프로토타입 체인의 종점이기 때문에 Object의 `__proto__`프로퍼티를 상속받지 못하고 사용할수 없음.
  - 따라서, `obj.__proto__`가아닌 `Object.getPrototypeOf(obj) `, `obj.__proto__ = value` 가 아닌 `setPrototypeOf(obj, value)`; 사용 

  ## 함수 객체의 protototype 프로퍼티

  - 함수 객체는 `prototype`이라는 프로퍼티를 가짐
  - 이 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가르킴.
  - 생성자 함수로서 호출할 수 없는 non-constructor인 화살표 함수, es6 메서드 축약 표현으로 정의한 함수는 prototype 프로퍼티를 소유하지 않음. 
  - 생성자 함수로 호출하기 위해 정의하지 않는 일반함수도 프로퍼티를 소유하지만 아무런 의미도 없음
  - 모든 객체가 상속받은  `__proto__` 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 동일한 프로토타입을 가르킴

  ## 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

- Object 생성자 함수가 아닌 리터럴로 생성된 함수도 Object 생성자 함수로 생성되었다고 나옴

```javascript
  const obj = {};
  console.log(obj.constructor === Object) //true
```

객체 리터럴에 의해 생성한 객체와 Object 생성자 함수에 의해 생성한 결국 객체로서 동일한 특성을 가짐 (생성한 함수는 생성 과정과 스코프, 클로저)

<table>
<tr>
  <th>리터럴 표기법</th>
  <th>생성자 함수</th>
  <th>프로토 타입</th>
</tr>
<tr>
  <td>객체 리터럴</td>
  <td>Object</td>
  <td>Object.prototype</td>
</tr>
<tr>
 <td>함수 리터럴</td>
 <td>Function</td>
 <td>Function.prototype</td>
</tr>
<tr>
 <td>배열 리터럴</td>
 <td>Array</td>
 <td>Array.prototype</td>
</tr>
<tr>
 <td>정규 표현식 리터럴</td>
 <td>RegExp</td>
 <td>RegExp.prototype</td>
</tr>
<table>

## 프로토타입의 생성 시점

- 프로토타입은 생성자 함수가 생성되는 시점에 함께 생성됨.
- 생성자 함수로써 호출을 할수 없는 함수 (non-constructor)는 프로토타입이 생성되지 않음

## 객체 생성 방식과 프로토타입의 결정

- 다양한 방식으로 생성된 모든 객체는 추상 연산 `OrdinaryObjectCreate`에 의해 생성됨
- 생성할 객체의 프로토타입을 인수로 전달 받음
- 인수로 전달받은 프로토타입을 생성한 객체의 내부 슬롯에 할당후 생성한 객체를 반환

## 프로토타입 체인 

생성자 함수로 생성된 인스턴스 객체가 `Object.prototype`의 메서드인 `hasOwnProperty`를 호출할수 있다는건 `Object.prototype`를 상속받았기 때문.

- 자바 스크립트는 객체의 프로퍼티에 접근하려고 할때 해당 객체에 접근하려는 프로퍼티가 없다면 내부 슬롯의 참조에 따라 부모 역활을 하는 포로토타입의 프로퍼티를 순차적으로 검색 (프로퍼티 체인)

프로토타입 체인의 종점은 `Object.prototype`

프로토타입 체인은 상속과 프로퍼티 검색을 위한 메커니즘

## 오버라이딩과 프로퍼티 섀도잉

- 오버라이딩 -> 상위 클래스가 가지고 있는 메서드를 하이ㅜ 클래스가 재정의하며 사용하는 방식
- 프로퍼티 섀도잉 -> 상속관계에 의해 프로퍼티가 가려지는 현상

## 프로토타입의 교체

- 프로토타입은 임의의 다른 객체로 변결할수 있음
- 프로퍼티 교체를 하고 constructor 프로퍼티와 생성자 함수 간의 연결을 재설정 해주지 않으면 연결이 파괴됨으로 주의해야함
- 상속 관계를 동적으로 변경시키는건 번거롭고 실수를 유발할수 있으니 직접 교체하는건 권장하지 않음. (직접 상속, 클래스를 이용)

## 직접 상속
- new 연산자가 없이도 객체를 생성할수 있음
- 프로토타입을 지정하면서 객체를 생성할수 있음
- 객체 리터럴에 의해 생성된 객체도 상속이 가능

```javascript
obj = Object.create(Person.prototype);
obj.name = 'Min';
console.log(Object.getPrototypeOf(obj) === Person.prototype); (true)
```

## 정적 프로퍼티/메서드

- 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출이 가능한 프로퍼티/메서드
- 생성자 함수에 추가한 정적 프로퍼티/메서드는 생성자 함수로 참조/호출, 
- 함수가 생성한 인스턴스로는 참조 할수 없음.

ex) `Object.create` - Object 생성자 함수의 정적 메서드, `Object.hasOwnProperty` - `Object.prototype` 의 메서드

## 프로퍼티 존재 확인

### in 연산자

- 객체 내에 특정한 프로퍼티가 존재하는지 확인

```javascript
  // key in object

  const animal = {
    name: 'Tom',
    species: 'Cat'
  };

  console.log ('name' in person) //true
  console.log ('toString' in person) //true - person 이라는 객체엔
   // toString 이 없지만 상위 객체인 Object의 프로퍼티이므로 상속받아 있다고 표시
  
```
`in`과 똑같이 작동하는 `Reflect.has`(ES6) 를 사용해도 똑같은 결과가 나옴

## 프로퍼티 열거 

- `for (변수선언문 in 객체)`

- 순회 대상이 객체의 프로퍼티뿐만 아니라 상속받은 프로토타입의 프로퍼티까지 열거 (프로토타입 체인상에 존재하는 모든 프로토타입의 프로퍼티)
- 열거할수 없도록 정의되어 있는 프로퍼티를 제외한 모든 프로퍼티를 순회하며 열거 (`[[Enumerable]]이 true`)











  