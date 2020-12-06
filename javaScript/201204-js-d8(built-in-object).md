# 빌트인 객체

## 자바스크립트 객체의 분류

- 표준 빌트인 객체 (Standard built-in objects/native objects/global)
  - Object, String, Number, Boolean, Symbol, Date, Array, Function
- 호스트 객체 (host objects)
- 사용자 정의 객체 (user-defined objects)

## 원시값과 래퍼 객체 

- 문자열, 숫자, 불리언 값에 대해 객체저럼 접근하면 생성되는 임시 객체를 래퍼 객체라 한다.
- 래퍼 객체의 처리가 종료되면 래퍼 객체의 내부 슬롯에 할당된 원시값으로 원래의 상태로 되돌리고 래퍼 객체는 가비지 컬렉션의 대상이 됨.

## 빌트인 전역 프로퍼티

- Infinity - 프로퍼티는 무한대로 나타내는 숫자값 Infinity를 갖는다
- NaN - 프로퍼티는 숫자가 아님.

## 빌트인 전역 함수

- eval - 전달받은 문자열 코드가 표현식이라면 eval 함수는 문자열 코드를 런타임에 평가하여 값을 생성, 전달받은 인수가 표현식이 아닌문이라면 문자열 코드를 런타임에 실행한다

- isFinite - 인수가 정상적인 유한수인지 검사하여 유한수면 true 무한수면 false. 

- isNan - 전달반은 인수가 NaN인지 검사하여 결과를 불리언 타입으로 반환
- parseFloat - 전달받은 문자열 인수를 부동 소수점 숫자, 실수로 해석하여 반환한다.
- parseInt - 전달받은 문자열 인수를 정수로 해석하여 반환한다.

- encode - 완전한 URL로 문자열로 전달받아 이스케이프 처리를 위해 인코딩함.
- decodeURL - 인코딩한 uri를 인수로 전달받아 이스케이프 처리 이전으로 디코딩
 