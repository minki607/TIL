> 몇가지 유용한 css 속성들과 기법들을 새로 배우면서 고정형 웹카페 레이아웃을 마무리 지었다.

---
### 항상 더 시멘틱한 마크업을 사용 
- 순서가 있는 리스트들은 `ul` 대신 `ol`을 사용해주는게 좋음. 리스트들의 스타일을 없애고(`list-style:none`) 새로 삽입한다해도 랭크처럼 순서가 중요한 리스트에는 `ol`을 사용해 명시해주는게 바람직함.

  - 리스트 스타일을 없앤뒤 새로운 디자인을 위해 숫자를 기입하는 방법 (`list-style: none 사용하지않음`). 주석 처리된 부분 참조.
  
  ```css
    .favorite-list {
    margin: 10px 0 0 0;
    padding-left: 0;
    overflow: hidden; /*리스트 밖으로 나가는 것들 숨김처리*/
  }

  .favorite-list li {
    margin-top: 8px;
    counter-increment: rank; /*카운터의 이름과 증가할 숫자의 단위 입력*/
    position: relative;
    
  }

  .favorite-list li:before { /*li 가상요소 (랭크)*/
    content: counter(rank); /*counter함수를 이용해 가상요소의 content 지정*/
    color: #fff;
    font-size: 1.2rem;
    display: inline-block;
    padding: 2px 5px; /*padding으로 기본 리스트 숫자값 밀어낸후 hidden 처리되게 하기 */
    margin-right: 5px;
    background-color: #999;
    border-radius: 2px; 
    position: absolute;

  }
  ```
  여기서 굳이 리스트 스타일을 없애주지 않고 padding 값을 줘서 `overflow:hidden` 처리를 한 이유는 `list-style: none`을 사용해 기본값을 없애주면 스크린리더가 순서를 읽어주지 않기 때문이다.
<br>

- `<address>` - 연락처 정보를 나타낼때

```html
  <address>
  <a href="mailto:mingeesuh@gmail.com">jim@rock.com</a><br>
  <a href="tel:+1073101077">(82) 10-7310-1077</a>
</address>
```
`mailto:` 메일을 바로 보낼수 있게 창이열림
`tel:` 전화걸기를 지원하는 디바이스에서 전화를 바로 걸수 있음 
  

- `<small>` - 저작권 정보 
```html
  <small class="copyright">
    Copyright since &copy; 2010 by Web Cafe CORPORATION ALL RIGHTS RESERVED      
  </small>
```
-  `<q>`- 인용문 , `<blockquote>` - 블록레벨 인용문  

```html
<q cite="https://w3.org/WAI/">         
  The power of the Web is in its universality. 
  Access by everyone regardless of disability is an essential aspect. 
</q>
<footer class="a11y-hidden">
  출처: W3C, http://w3.org/WAI/
</footer>
```
 무언가 인용시 `cite`를 기입하는 습관을 꼭 갖는게 중요. 더 명확한 출처를 남기기 위해 a11y-hidden 처리된 footer안에 추가적으로 기입하기도함.
 `<q>`사용시 기본으로 <strong>"</strong> 가 인용문의 기호로 붙게 되는데 아래의 css 속성을 이용해 변경가능하다.
 ```css
  q { quote: "[" "]" } /*[이 괄호안에 인용문이 들어가게됨]*/
 ```

 ---

 ### 다양한 CSS 기법을 통해 접근성 향상시키기

- Position trick
<br>
  
  저번에 IR기법에 대해 알아봤는데 오늘은 그를 조금 변형한 position trick에 대해 알게되었다.

  배경 이미지의 경우 대체 텍스트를 삽입하는게 불가능해 IR기법을 통해 텍스트를 숨김 처리하는 방식으로 많이 사용했었는데 만약 배경 이미지가 정상적으로 로딩되지않는다면 배경이나 텍스트 둘다 보이지 않는 문제가 발생한다.

  이때 position을 사용한 이미지 배치 방법을 사용한다면 접근성면에서도 우수하고 css가 로딩 되지 않는다 하더라도 이미지의 대체 텍스트의 효과를 낼수 있다. 

  ```html
    <h2 class="slogan-heading" title="웹카페에서 웹표준을">슬로건</h2>
  ```
  ```css
  .slogan-heading{
    height: 83px; 
    width: 110px; 
    font-size: 1.4rem;
    font-weight: 400;
    text-align: center;
    line-height: 83px; /*text-align과 line-height 를 이용해 슬로건이라는 텍스트를 중앙 배치*/
  }

  ```
  위에선 텍스트를 중앙에 배치해줬지만, 
  이미지 배경에 따라 안보일만한 위치에 정렬시켜주면 됨.
  <br>

  이제 가상요소 클래스를 사용해 배경을 넣어주고 position값을 주면 텍스트가 아래에 존재하지만 화면상 보이지 않게됨.
  <br>
  ```css
  .slogan-heading::after{
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background: url(./images/coffee.png) no-repeat 0 0;
  ```

  아주 유용하게 쓰일수있지만 배경 이미지에 따라 적용여부가 결정된다는 단점이있음.
<br>
- 본문 바로가기 제공

본문 바로가기 기능은 키보드를 사용해 네비게이션을 하는 사람들에게 아주 유용한 기능이기 때문에 접근성을 고려한 웹을 만든다면 필수 요소중 하나임.

마크업은 아래와 같이 정말 간단하게 작성할수있음. 보통 body태그 바로 아래 위치시켜 tab을 눌렀을씨 제일먼저 focus를 받을수있게함.
```html
 <div class="skip-nav" >
    <a href='#content'>본문 바로가기</a>
</div>
```
본문 바로가기를 누르면 바로 #content(본문 섹션)으로 갈수 있도록 설정을 해준뒤 css를 통해 skip-nav가 포커스를 받을때만 나타날수 있게 해주면 됨.

```css

/*본문 바로가기 링크는 상단에 고정시키고 height 0을 줘서 보이지 않게해줌*/
.skip-nav a {
  position: absolute;
  width: 100%;
  background-color: #000;
  color: #fff;
  text-align: center;
  top: 0;
  left: 0;
  z-index: 10;
  height: 0;
  overflow: hidden;
}

/*focus를 받으면 auto값을 줘서 텍스트의 크기 만큼 보일수 있게해줌*/
.skip-nav a:focus {
  height: auto;
  padding: 10px 0;
}

```



