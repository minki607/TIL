### 반응형 웹디자인 (Responsive Web Design)

##### padding, margin을 통해 텍스트 정렬시 em, rem을 사용

고정형 레이아웃을 만들때 line-height를 사용하여 텍스트를 수평 정렬하는 방식을 자주 써왔지만,

반응형에서는 em같은 상대적 단위를 사용해서 폰트사이즈의 사이즈가 변해도 유동적으로 정렬이 가능하게 해주는게 좋음

##### 더 많은 aria 속성들

- `aria-live` - 새롭게 업데이트된 정보를 사용자에게 즉시 알릴수 있음. 예를들어 사용자가 특정 작업을 했을때 돌아오는 상태 메세지값을 표시하기 위해 aria-live 속성을 사용해 특정 영역을 '라이브'로 표시할수 있음
  - `aria-live="polite"` - 작업을 맞추는 즉시 사용자에게 변경 사항을 알려줌
  - `aria-live="assertive"`- 수행 중인 모든 작업을 중단하고 변경 사항을 즉시 알림

- `aria-modal` - 값이 true일시 모달 콘텐츠임을 명시해 다른콘텐츠의 사용을 배제시킴 (클릭, hover 등). 기본값은 false로 모달창이 아닌상태.
- `aria-pressed` - 버튼의 상태를 명시. true or false값을 적어 toggle 버튼의 기능을 구현 할수있음. `aria-pressed='false'로 지정할시 스크린 리더에서는: Toggle. Button not pressed.로 읽힘.
- `aria-haspopup` - 현재 요소에 (숨겨진)팝업창이 있다는걸 명시해줌. 
- `aria-current`- 현재 맥락과 일치하는 항목을 의미. 값은 여러개 `page|step|location|date|time|true|false(default)`오늘은 `page`속성을 써서 현재 페이지를 시각적으로 강조. 


#####  column 속성을 사용해 다단 레이아웃 만들기

- column-width: 단의 너비를 지정. 
- column-count: 단의 개수를 지정. 
- column-gap: 단 사이의 간격을 지정
- column-rule: 단과 단 사이에 구분선 표시
`div { column-rule : #000 solid 2px ; }`


##### table을 속성을 사용해 테이블 레이아웃 만들기


`<table>`	테이블
`<caption>`	테이블의 캡션
`<thead>`	테이블 헤더
`<tbody>`	테이블 본문
`<tfoot>`	테이블 푸터
`<tr>`	테이블 행
`<th>`	헤더 셀 (제목요소)
`<td>` 데이터 셀 (일반적인 데이터)
`<colgroup>` 그룹 열
출처: https://css-tricks.com/complete-guide-table-element/

table scope - 해당 제목과 관련있는 데이터들을 연결해줌. 