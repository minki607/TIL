# String

## String 생성자 함수
- new 연산자와 함께 호출해 String 인스턴스를 생성가능
- 인수를 전달하지 않으면 빈문자열을 할당한 string 래퍼 객체를 생성

```javascript
const strObj = new String('Suh');
console.log(strObj); //[String: 'Suh']

// 유사 배열 객체이면서 이터러블이기때문에 인덱스를 사용해 문자에 접근가능
console.log(strObj[0]);

// 하지만 원시값이므로 변경이 불가능
strObj[0] = 'M';
console.log(strObj) // 'Suh'

// 문자열의 문자 개수를 반환하는 length 프로퍼티도 쓸수 있음

strObj.length = 3;
```

## String 메서드

- String 래퍼 객체는 읽기 전용 객체로 제공
- 따라서 모든 메서드는 String 래퍼 객체를 직접 변경하지 못하고 새로운 문자열을 생성하여 반환

## String.prototype.indexOf

- 인수로 전달받은 문자열을 검새후 첫번째 인덱스 반환.
- 실패시 -1 반환

```javascript
  strObj.indexOf('f') // -1
  strObj.indexOf('u') // 1

```

## String.prototype.search

- 문자열에서 인수로 전달받은 정규표현식과 매치하는 문자열의 인덱스 반환

## String.prototype.includes

- 문자열에 인수로 전달받은 문자열이 포함되어있는지 확인하여 불리언값 반환

## String.prototype.startsWith

- 전달된 문자열로 시작하는지 확인하여 그 결과를 반환 t/f

##  String.prototype.endsWith

- 전달된 문자열로 끝나는지 확인하여 그 결과를 반환 t/f

## String.prototype.charAt

- 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환

## String.prototype.substring

-  문자열에서 첫 번째 인수로 전달받은 인덱스에 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 부분 문자열을 반환

```javascript
const str = 'Hello World';

// 인덱스 1부터 마지막 문자까지 부분 문자열을 반환한다.
str.substring(1); // -> 'ello World'
```

## String.prototype.slice

- substring 과 동일하게 작동. 
`str.slice(-5); // ⟶ 'world'`

## String.prototype.toUpperCase

- 대상 문자열을 모두 대문자로 변경한 문자열을 반환

## String.prototype.toLowerCase

- 대상 문자열을 모두 소문자로 변경한 문자열을 반환

## String.prototype.trim

- 문자열 앞뒤에 공백 문자가 있을 경우 제거한 문자열을 반환

## String.prototype.repeat

- 문자열을 인수로 전달받은 정수만큼 반복해 새로운 만자열을 반환 

## String.prototype.replace

문자열에서 첫번째 인수로 전답랃은 문자열 또는 정규표현식을 검색해 두번째 인수로 전달한 문자열로 치환한 문자열 반환

## String.prototype.split

문자열에서 첫번째 인수로 전달한 문자열 또는 정규표현식을 검색해 문자열을 구분한후 분리된 문자열로 이루어진 배열을 반환





