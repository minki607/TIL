# HTML5 Markup

오늘은 html5의 역사와 구조에 대해 간단하게 알아보았고, 직접 html 구조를 설계해보며 html5에 새롭게 추가되었던 기능들을 하나하나 살펴보았다.

## HTML5의 완전한 표준의 정착
  ![](https://t1.daumcdn.net/cfile/tistory/995430485B5ABD2533)

  
### W3C(World Wide Web Consortium) ###

웹의 표준을 정의하는 국제 컨소시엄

 ### WHATWG(Web Hypertext Application Technology Working Group) ###
 
주류 브라우저 Vendor (애플, 구글, 마이크로소프트, 모질라) 네 회사 중심으로 만들어져 돌아가는 웹 기술 표준화 조직
 
### html 5 (Markup Language) ###
- XHTML 1.0 
     -  엄격한 문법검사 (하위 호환성을 지원하지 않아 표준화에서 멀어짐)
- HTML 4.01
	- 안정된 표준의 html 버전 (기술적인 한계에 부딫혀 발전이 멈춤)

WHATWG에서 HTML을 계승하는 언어를 개발 
XHTML을 추진화하고 있던 W3C도 XHTML을 표준에서 탈락 시키고 WHATWG와 협력해 HTML5 버전으로 재탄생 시킴

# HTML5에 추가/수정된 점

### 새롭게 등장한 콘텐츠 모델 / 카테고리

- 명확한 구조 설계 및 구성을 위해 카테고리를 정의. 각 요소별로 비슷한 성격을 가지고 있는것끼리 그룹화


![HTML 마크업 | 웹접근성과 웹표준](https://seulbinim.github.io/WSA/images/markup/content-model.png)
### 섹셔닝 루트 

- 독립적인 컨텐츠를 분리할수 있는 특정 요소의 카테고리
- body, figure, blockquote, details, fieldset, td 요소가 있음

### 메타데이터 컨텐츠 

- 문서와 문서간의 관계를 설정

### 그 외 다양한 컨텐츠들을 나타내기 위한 요소들
- heading contents:  &lt;h1> ~ &lt;h6> 
- phrasing contents : &lt;a>, &lt;br>, &lt;span> 등 
- embeded contents: &lt;audio> &lt;iframe> &lt;video>등
- interatice contents: &lt;select>, &lt;textarea>
- palpable contents: &lt;div>, &lt;figure> &lt;canvase>
	

### 아웃라인 알고리즘 

- 웹 페이지의 정보 구조를 판별할 수 있는 개념
- 많은 요소(section, article, aside) 등이 추가된 이유

### API
- 다양한 API(Application Programming Interface) 추가
- 자바스크립트 기술을 좀 더 편리하게 이용할 수 있도록 지원
- ex) 오프라인 웹 구현을 위한 API 
	- Web Storage 
	- Web SQL Database/Indexed Database
	- Application Cache


## HTML 마크업의 기초 

**태그(tag)** 
 기본 형식: &lt;div>&lt;/div> (여는 태그, 닫히는 태그)
 빈 요소: &lt;br> 또는 &lt;/br> 
 **속성(attribute)**
 &lt;input **type**='text' , **id**='user' **required**> (required는 논리 속성)
 
  

## HTML 주의사항

- 대소문자의 사용상관없지만 주로 소문자 사용
- 빈 요소 (self closing tag) - &lt;/br> (slash를 안넣어도 무관하지만 여러 프레임워크가 이 형식을 사용중이므로 익숙해지는게 좋다고 한다)

- 잘못된 중첩 사용 불가능 ( 시작 태그와 종료 태그의 중첩에 문제가 발생하지 않도록 해야함)
- 중복 속성 사용 불가능
- 문자 참조 - < , > , & 의 경우 character entity name이나 entity code로 변환하여 사용
  
- 논리적인 순서 (테이블 x)
- 예) 아이디 -> 비밀번호 -> *로그인 정보 저장* -> 로그인 
- 시맨틱 마크업 
  - 컨텐츠를 잘 이해할수 있도록 의미있는 마크업 사용
 - 네이밍(naming)
	 - css 방법론
	 - BEM 참조 	




