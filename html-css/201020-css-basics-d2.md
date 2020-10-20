

> 어제 마크업 했던 html에 css를 입혀보며 선택자들, 속성 그리고 접근성에 관해 알아보았다. 많이 알고 있던 주제라 생각했지만 막상 강의를 들어보니 모르는 부분이 더 많았던거 같다. 이전에는 접근성에 대해 깊게 생각해보지 않았었는데 사소하다고 생각했던것이 많은 차이를 만드는거 같아 앞으로는 더욱 신경 써보려한다.



# Box Model
모든 html 요소는 박스(box) 형태의 영역을 가짐  
**이 BOX 는 content, padding, border, margin으로 구성**
box-sizing 프로퍼티를 이용해 박스모델을 정의할수 있음 

## content-box
- 요소의 너비와 높이를 **콘텐츠 영역**을 대상으로 함(기본값)
- :warning: 지정한 콘텐츠 영역보다 실제 콘텐츠가 크면 콘텐츠 영역을 넘침
- 따라서 padding, margin, border 그리고 컨텐츠의 width, height을 전부 고려하며 영역을 지정해야함

## box border-box

-  콘텐츠 영역, padding, border가 포함된 영역을 대상으로 지정가능 
- padding, border의 사이즈를 고려하며 전체 영역의 값을 지정하지 않아도 됨


## CSS 알아두면 좋은 속성/개념들

* `*{}` 전체 요소 선택자
  * 기본으로 적용된 css를 reset시키거나 박스모델 정의할때 유용함
  * 더 좋은 성능을 위해선 조금 더 구체적으로 명시하는게 좋음 


	```css
			body *, body *::before, body *::after{
		    box-sizing: border-box;
		    } /*::before, ::after는 주로 생략 되기도 하지만 가끔 브라우저마다 가상선택자에 default 스타일이 있을수도 있기에 명시 */
	```
 * float 속성
    - 블록 level의 객체를 정렬하기 위해 많이 쓰임. 블록은 기본적으로 가로 전체를 차지하기 때문에 다른 블록요소와 나란히 정렬하기 위해 float를 이용해주는 경우가 많음 
    - display: flex를 많이 쓰곤 하지만 이를 제대로 지원하지 않는 브라우저 (IE 등)이 몇 있어 아직도 **cross-browsing**을 위해 자주쓰임

		```css
		div{float:left;} /* 문서를 주로 왼쪽에서 오른쪽으로 읽기 때문에 제일 많이 쓰임 */
		div{float:right;}
		div{float:both;}
		```
	- :warning: float 프로퍼티를 사용하면 다음 요소가 원치않게 비어있는 자리에 올라오고 자식요소가 전부 float 상태이면 부모가 **height 값**을 인지하지 못함.  
	- 이를 해결하기 위해 
		 
		```css
		.content{overflow: hidden;} 
		/* 자식요소가 float인 부모에게 이 값을 주면 자식을 담아냄
		단 내용이 넘치면 컨텐츠가 보이지 않음 */	
		.content{overflow:auto;} 
		/* 컨텐츠가 넘쳐도 보이지만 원치않는 스크롤이 생길수 있음 */
		.empty-tag{clear:both;}
		/*빈 요소를 생성해 float 를 clear해 취소해줌 마크업의 흐름을 깰수 있어 권장하		지 않음*/
		.content::after{display:block; content:''; clear:both}
		/*부모에게 가상요소를 만들어 만들어 주고 블록레벨 요소로 만들어줘 가로 전체를 차지	하게함, 만약 display:flex를 같이 사용하게 되면 가상 클래스도 하나의 요소로 인식해 정렬이 힘들수도 있음*/
		``` 
				
		 
 :warning: 부모요소에게 fixed height를 주는건 최대한 피하는게 좋음. fixed height 값은 컨텐츠가 추가되거나 바뀔일이 없는 요소에만 사용하고 되도록 자제
 
최소높이를 줘야할땐 (min-height)
position: relative , float: left,right-기존 normal flow를 유지
position: absolute:  상위 요소중 position이 static이 아닌 요소를 기반으로 포지션함.


# 접근성 


- '|' 같은 문자열 divider를 사용할 경우 screen reader가 인식하지않도록 `aria-hidden = true` 속성을 사용하도록 권장 

- 보통 링크는 li 자체가 아닌 anchor 태그에게 주고 clickable 한 면적을 확장시키기. 

# 그 외 

- 인라인, 인라인 블록요소에서 원치 않는 공백문자 handling 하는법
	- 태그를 붙혀서 닫기
	 ```html
		<ul>  
			<li>one</li  
			><li>two</li  
			><li>three</li>  
		</ul>  <!--tag를 붙혀서 닫기-->
	 ```
	
	- 응수 마진 
	- closing tag 생략 (추천 하지 않음) 
	- 부모 요소 font-size: 0으로 하고  li 의 font-size: 재정의
	
		```css 
		nav {  font-size:  0;  }  
		nav a {  font-size:  1.4rem;  }  
		```
  