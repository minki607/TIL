# Number

- 표준 빌트인 객체로 원시 타입인 숫자를 다룰때 유용한 프로퍼티와 메서드를 제공

- new 연산자와 함께 호출시 [[NumberData]] 내부슬롯에 인수로 전달받은 숫자를 할당한 Number 래퍼 객체를 생성

- new 연산자 없이 호출시 Number 인스턴스가 아닌 숫자를 반환

## 프로퍼티

- `Number.EPSILION`
    - 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이와 같음
    - 부동 소수점으로 인해 방생하는 오차를 해결하기 위해 사용

- `Number.MAX_VALUE`
    - 자바스크립트에서 표현할 수 있는 가장 큰 양수
    - 이 값 보다 큰 값은 Infinity 

- `Number.Min_VALUE`
    - 자바스크립트에서 표현할 수 있는 가장 작은 양수 값
    - 이 값 보다 작은 값은 0

- `Number.MAX_SAFE_INTEGER`
    - 자바스크립트에서 가장 안전하게 표현할수 있는 가장 큰 정수

- `Number.MIN_SAFE_INTEGER`
    - 바스크립트에서 가장 안전하게 표현할수 있는 가장 작은 정수(음수)

- `Number.POSITIVE_INFINITY`
    - 양의 무한대

- `NUMBER.NEGATIVE_INFINITY`
    - 음의 무한대

- `Number.NaN`
    - 숫자가 아님
    - window.NaN 가 같음

## 메서드

- `Number.isFinite`
    - 인수로 전달한 값이 유한수인지 무한수인지 검사하여 결과를 불리언으로 반환.
    - `Number.isFinite(Infinity) // false`
    - window.isFinite 가 달리 인수를 숫자로 암묵적 타입 변환하지 않음

- `Number.isInteger`
    - 인수로 전달된 숫자값이 정수인지 아닌지 검사해서 불리언 값으로 변환
    - 인수를 숫자로 암묵적 타입 변환 하지 않음.
    - `Number.isInteger(0) // true`
    - `Number.isInteger('123') // false`

- `Number.isNaN`
    - 인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 불리언값으로 반환
    - window.isNaN과는 달리 인수로 전달된 인수를 숫자로 암묵적 타입변환하지 않음.

- `Number.isSafeInteger`
    - 인수로 전달된 값이 안전한 정수인지 검사하여 결과를 불리언 값으로 반환

- `Number.prototype.toExponential`
    - 숫자를 지수 표기법으로 반환하여 문자열로 반환
    - 숫자 리터럴을 쓸경우 그룹 연산자를 사용 권장

- `Number.prototype.toFixed`
    - 숫자를 반올림하여 문자열로 반환. 반올림하는 소수점 이하 자리수를 나타내는 0~20 사이의 정수값을 인수로 전달가능 (기본 0)

- `Number.prototype.toPrecision`
    - 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환

- `Number.prototype.toString`
    - 숫자를 문자열로 변환하여 반환
    - 인수 생략시 기본값 10진법이 지정