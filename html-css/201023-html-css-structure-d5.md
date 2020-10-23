
## 세부 콘텐츠 구조 설계

- 메뉴 앞 아이콘 가상요소 vs span (`<span class="open-right-icon" aria-hidden="true">`) 무엇을 써야하는가?

오늘 수업중 *fontello나 fontawesome* 같은 폰트 아이콘을 쓸때 가상요소를 써야하는지 span에 지정된 class이름을 써야하는지에 관한 질문이 나왔다. 보통 가상요소의 content 값은 screen reader에 읽히기 때문에 `<span>`을 쓰고 `aria-hidden` 속성을 사용한다. 하지만 content: `"\f192"` 처럼 앞에 \가 붙으면 읽지 않아 이 방법도 aria-hidden 속성을 준 span이랑 똑같이 사용가능하다.

   ```css
	.sub-menu  a::before {
	   content: "\f192";
		font-family: 'fontello';
		display: inline-block;
		width: 1em;
		margin-right: .2em
	}
   ```

가상요소를 선택하면 자바스크립트 없이도 `hover` 했을시 아이콘을 변경해주는 이벤트를 구현할수 있다.

 ```css
.sub-menu  a:hover::before, .sub-menu  a:focus::before {
content: "\e800";
}
```

상황에 맞게 번갈아 쓰면 될듯하다.

- 추가적인 정보를 입력할때는 title 전역 속성을 사용한다. 많은 사람들이 title을 label 대신 쓰곤 하지만 접근성면이나 유저 편의성에선 이를 권장하지 않음 (label을 클릭하면 input으로 바로가는 편의성).

- `fieldset` - 연관성 있는 form 관련 요소들을 그룹해줌 (필수,선택 필드등). 폼을 효과적으로 **계층화** 시킬수 있음. legend 와 같이 사용가능. 필수는 아니지만 접근성의 측면에선 아주 유용함.
- `legend` fieldset 요소의 제목 '로그인 폼 , 회원가입 폼' 등. (시각작인 면에선 필요없는 부분이므로 주로 .a11y-hidden같은 방법을 통해서 숨김 표시 처리를 해줌)

- font-size가 12px 보다 낮을시 접근성, SEO에서 낮은 점수를 받을수 있음

- 버튼의 padding값은 브라우저마다 조금씩 다르기 때문에 재정의 해주는게 좋음

- `_blank` 새로운 창에서 링크 띄우기. 앞에 _를 생략하고 그냥 `<a target='blank'>`을 줘도 새로운 창이 띄어지는것처럼 보이지만 blank라는 창을 찾고 없으면 새로운 blank라는 창을 띄우는 방식임. 똑같은 링크를 여러번 클릭해보면 계속 처음 열린 창에 띄워지는걸 볼수 있음. 

- `_self` 기본창에서 링크 띄우기

- `section` - 명시적인 outline을 생성할때 주로 쓰임 
- `aside` - 부가적인 정보/ 없어지더라도 main의 내용을 이해하는데 지장이 없어야함. 주로 광고에 많이 쓰이곤함
- `article` - 재사용할 독립적인 컨텐츠. section과 article의 명확한 구분은 없어 많이 헷갈려함.

-  용어를 정의할때는 `<dl>` - 영역 `<dt>` - 용어 `<dd>` - 정의 . 최신 5.2 html 버전에선 div로 `dl dt dd` 영역을 **함께** wrapping 할수 있음. (따로는 불가능)