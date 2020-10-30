> 오늘은 이벤트 섹션과 관련 사이트 섹션을 만들면서 웹카페 마무리 작업에 들어갔다. 오늘도 역시 접근성에 관련된 정보가 다수 나왔는데 모든 환경에서 정보제공을 동일하게 하려면 정말 많은 노력이 필요함을 다시한번 느꼈다. 예전에는 정말 생각하지도 못했던, 나만의 환경이 아닌 다른 사람을 고려하면서 만드는 방법을 이제라도 점차 알아가는것 같아 다행이다.


### 이미지의 대체 텍스트는 명확하게

지금까지 이미지태그의 `alt`속성은 그저 이미지가 로드 되지않았을때 대신 화면에 보여질 설명을 명시해주는 용도라 생각하고 많은 신경을 쓰진 않았던거 같다. 그래서 보통 `alt="logo"`, 나 `alt="article image"` 처럼 전반적인 이미지의 의도를 명시해주는 용도로 써왔었다.

하지만 대체 텍스트는 가능한 이미지와 동일한 내용을 전달해줘야한다고 한다. 예를 들어 이벤트 경품에 관한 이미지의 대체텍스트로는 `alt="이벤트 경품 : 웹표준 핵심 가이드북2 도서 증정"` 이런식으로 대체 텍스트만으로도 온전히 이미지의 의도가 설명될수 있을 만큼 말이다. 

### aria-labelledby

현재 요소를 레이블하는 요소를 식별하기 위해 쓰임. 주로 form, radio-box에 많이 쓰이기도 하지만 figure img의 대체텍스트의 용도로도 쓰일수 있음. 

```html
 <figure class="news-article-thumbnail">
    <img aria-labelledby="newsArticleThumbnail" src="https://cdn.mos.cms.futurecdn.net/mEuBJTDhXuTfSKdLefzSKg.jpg" alt="" >
    <figcaption id="newsArticleThumbnail">
    들판위를 걷고 있는 기린
  </figcaption>
</figure>
``` 
`figure`는 `figcaption`과 함께 쓰이는데 이는 이미지에 관한 부가 설명을 제공하므로 이 요소의 id값을 `img`의 aria-labelledby 속성에 명시하여 관계를 형성해줄수 있음(이로써 대체텍스트가 없어도 figcaption이 그의 역활을 대신 해준다는걸 인지할수 있음).

### 정지 기능 제공

가끔 사이트를 방문해보면 메인 배너나 이벤트 배너들이 자동으로 재생되는걸 볼수 있는데 여기서 접근성을 고려하지 않는 사이트를 간간히 볼수 있다. 

저시력자나 지적장애인들은 문서를 읽고 이해하는데 더 많은 시간이 필요할수 있음으로 자동으로 변경되는 콘텐츠를 제어할수 있는 수단도 함께 제공해야 한다고 한다.

보통 재생및 정지 버튼을 함께 제공하거나 마우스가 올려졌을시 멈춰지는 방법을 많이 선택한다.

### IR기법(Image Replacement)

의미있는 이미지를 배경처리하고 그에 상응하는 내용을 텍스트로 기입해 역활이나 의도를 명시하는 방법 

텍스트는 <strong>스크린리더</strong>에서만 읽히고 디자인상 화면에 보이지 않아야 함으로
<s>`visibility: hidden과 display: none;`</s>이 아닌 다음과 같은 방법을 채택할수 있다. 

- `text indent`
- `padding`
- `.a11y-hidden`
- `z-index`



#### text-indent

들여쓰기 속성을 사용해 텍스트를 버튼 영역 밖으로 밀어낸뒤 `overflow:hidden`처리를 하는 방식이다. `white-space: nowrap`과 같이 사용해야 줄바꿈이 되지않으면서 넘치는 영역이 숨김 표시가 된다.


 ```html
 <button type="button" class="btn-prev">이전 목록 보기</button>
 ```
```css
.btn-prev {
  background: transparent url(./images/back_forward.png) 0 0 no-repeat;
  border: 0;
  width: 19px;
  height: 18px;
  text-indent: 20px;
  white-space: nowrap;
  overflow: hidden;
}
```

#### padding

비슷한 방법으로 최소한 버튼의 높이값만큼 padding-top을 주고 넘치는 영역을 `overflow:hidden` 처리를 할수도 있다.

#### .a11y-hidden

버튼안에 자식요소를 추가해 그 요소에게 a11y-hidden 클래스를 추가해 화면에 보이지 않게 해주는 방법도 있다.

 ```html
 <button type="button" class="btn-prev">
  <span class="a11y-hidden">이전 목록 보기</span>
 </button>
 ```

```css

.a11y-hidden{ 
  margin: 0;
  position: absolute;
  width: 1px;
  height: 1px;
  overflow: hidden;
  clip-path: polygon(0 0, 0 0, 0 0);
  clip: rect(0 0 0 0);
  clip: rect(0,0,0,0);
}

```

##### z-index 

오늘 배우진 않았지만 검색을 통해 알게된 또하나의 방법. 텍스트에 z-index 속성값을 음의정수로 주어 맨 뒤에 배치하는 방법. css가 정상적으로 로드 되지 않을때 숨겨진 텍스트가 화면에 노출될수도 있다고 한다.   


--- 

많은 사람들이 오해하고 있는게 있는데 모든 환경에서 동일한 정보를 제공하기 위해 UI또한 똑같을 필요는 없다는것이다. 브라우저마다 다른 환경을 가지고 있고 그에 따라 최적화된 방법으로 정보제공을 하기 위해서는 UI가 세부적으로 변경되는건 어찌보면 당연한 일이라고 생각한다.