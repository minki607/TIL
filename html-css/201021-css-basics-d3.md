# CSS 포지션 속성 



 **position이란?** 
* 태그들의 위치를 결정하는 css 속성
* static, relative, absolute, fixed, 

포지션을 이미 잘 정리해놓은 사이트가 많아 간단히만 정리해보았다.

## static 

모든 태그들은 기본적으로 position: static값을 기본으로 함. 
왼쪽에서 오른쪽으로 , 위에서 아래로 쌓이는 속성을 갖고있음.

static일때는 top, left, right, bottom 속성이 명시 되어있다 해도 무시됨

<iframe height="332" style="width: 100%;" scrolling="no" title="position static" src="https://codepen.io/minki607/embed/preview/pobEZyg?height=332&theme-id=light&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/minki607/pen/pobEZyg'>position static</a> by Min Gee
  (<a href='https://codepen.io/minki607'>@minki607</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## Relative

`position: relative` 값을 주었을때 각각의 태그가 static이였을때를 기준으로 top, left, right, bottom 값을 줘서 위치 조절을 할수 있음 

<iframe height="265" style="width: 100%;" scrolling="no" title="qBNavEV" src="https://codepen.io/minki607/embed/qBNavEV?height=265&theme-id=light&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/minki607/pen/qBNavEV'>qBNavEV</a> by Min Gee
  (<a href='https://codepen.io/minki607'>@minki607</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 각각의 방향을(top, left, right, bottom) 기준으로 태그 안쪽 방향으로 이동. 

## Absolute

static 속성을 가지고 있는 부모 요소 기준으로 움짐임. 만약 static이외의 속성을 가지고 있는 부모 요소가 없다면 브라우저 기준으로 위치가 산출됨.

<iframe height="265" style="width: 100%;" scrolling="no" title="QWEKPZm" src="https://codepen.io/minki607/embed/QWEKPZm?height=265&theme-id=light&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/minki607/pen/QWEKPZm'>QWEKPZm</a> by Min Gee
  (<a href='https://codepen.io/minki607'>@minki607</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## Fixed

특정 위치에 고정. 매번 같은 위치에 고정이 되어있음

## Sticky

기준점을 넘지 않았을 경우 relative 속성을 준것처럼 작용하다가 , 그 값을 넘길시 fixed 속성과 같이 동작.

---

## 유용한 팁들  

- `<nav>` 요소는 주요 링크/서비스를 나타날때만 사용하는 편이 좋다고한다. 전에는 nav 태그를 여러번 사용하곤 했는데 앞으로는 중요 링크들만을 담는 용도로 사용하고 나머지는 `<ul>` 태그에 클래스 이름을 넣어서 써야겠다.

```html
	<header> <!-- 전체를 header로 wrapping -->
		<ul class='sub-menu'><!-- sub-menu 는 ul로 작성 --></ul>
		<nav class='navigation'><!-- 주요링크는 nav로 작성 --></nav> 
	</header>
```

- 접근성 측면에서 필요하지만, 시각적으로 표현될 필요가 없는 경우 

```css
	.a11y-hidden {
		position: absolute; 
		clip-path: polygon (00,00,00)
		width: 1px; /*최소한의 크기를 줘야 스크린 리더가 이를 인식해 기계적으로 접근가능. 0*/
		height: 1px; 
		overflow: hidden;
	}
```

 `display: none`,  `aria-hidden`은 기계적으로 접근이 불가능해 접근성에는 유용하지 않음.

- `<div>, <span>`은 필요할때만 쓰고 용도와 맞는 태그를 선택하는게 중요.
	ex) 무언가 누르는 용도로 쓰인다고 하면 `<button>`태그를 사용해 접근성에 용이한 `aria-pressed, aria-haspopup, aria-expanded`등  고유 속성을 사용

- 아이콘 삽입방법 - 이미지(해상도가 깨질수 있어 추천 하지 않음 , 폰트 아이콘 , svg등
- `!important`는  재정의가 불가능하니  (!important로만 재정의) 남발하는건 옳지 못함. 많은 프레임워크의 스타일을 바꾸기 어려운것도 !important로 정의된 다수 있어서라고한다.