### 반응형 웹디자인 (Responsive Web Design)

##### 비디오는 21:9, 16:9, 4:3 비율을 유지

보통 데스크탑의 비디오 비율은 16:9지만 상황에 따라 21:9 또는 4:3 비율로도 쓰이니 그에 맞게 비디오 영역 크기를 지정해줘야함.

반응형 디자인이니 `width:100%`를 기준으로 height값을 아래와 같이 계산해줄수 있음.

```
4:3 일경우 3/4 = 0.75 = 75% 
16:9 일경우 9/16 = 0.5625 = 56.25%
21:9일 경우 9/21 = 0.4285...% = 42.85%
```

4:3의 비율을 유지하기 위해선 보통 `height: 75vw` 이런식으로 정의해줄수 있겠지만 동영상의 너비가 화면을 꽉차는 레이아웃이 아닐시에는 정해진 비율에 맞게 높이가 변하지 못하는 상황이 발생할수도 있음.

따라서 `height`가 아닌 `padding-bottom`또는 `padding-top`을 이용해 해결할수 있음.

height의 기준은 부모 태그의 높이지만 
padding의 기준은 자신의 너비를 기준으로 설정 된다. (%사용시)

이런식으로 padding을 주게 되면 iframe이 영역밖으로 밀려나가기때문에 부모 영역에게 position: relative를 주고 iframe에게 absolute를 줘서 영역을 나가지 않도록 해줘야함. 

```css

.iframe-wrapper {
  width: 100%;
  position:relative;
  height: 0 !important; /*혹시 높이가 들어가게 되면 padding값과 합쳐져 비디오 비율이 무너질수 있기 때문에 0으로 최우선 처리해줌 */
}

/*요구되는 비율에 맞춰 쓸수있게 클라스를 따로 지정*/
.iframe4-3{
  padding-top: 75%;
}
.iframe16-9 {
  padding-top: 56.25%;
}

/*비디오가 부모요소를 꽉 채울수 있도록 설정*/
.iframe-wrapper iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

```

##### 변수(사용자 지정 속성)을 사용해 코드 재사용성과 가동성 높히기  

CSS에서도 기본적으로 변수 기능을 제공하는데 (IE에서는 지원하지 않음) ,
이를 적절하게 활용하면 코드의 재사용성과 가독성을 높일 수 있음.

```css
:root {
 --theme-primary: #24388d;
}
```

위에 경우에는 의미와 결과를 예측하기 어려운 색상코드에 대해 의미를 부여해 쉽게 알아보고 사용할수 있게 해줌. 처음에는 좀 더 많은량의 코드를 써야해서 불필요하게 느껴질수 있지만 프로젝트가 복잡해질수록 유지보수면에서 강력한 효과를 낼 수 있음.

지정한 변수를 사용하기 위해선 `var()`함수를 사용
```css
.container {
  background-color: var(--theme-primary);
}
```

##### 접근성을 고려하며 비디오를 삽입하기

```html
<video controls>
  <source src="https://storage.googleapis.com/webfundamentals-assets/videos/chrome.webm" type="video/webm" />
  <source src="https://storage.googleapis.com/webfundamentals-assets/videos/chrome.mp4" type="video/mp4" />
  <track src="chrome-subtitles-en.vtt" label="English captions"
         kind="captions" srclang="en" default>
  <track src="chrome-subtitles-zh.vtt" label="中文字幕"
         kind="captions" srclang="zh">
  <p>This browser does not support the video element.</p>
</video>
```
출처: https://web.dev/media-accessibility/

브라우저마다 지원할수 있는 확장자가 다르니 source를 이용해 갖고있는 모든 확장자 파일의 링크를 걸어두면 지원되는 확장자를 골라 비디오를 재생 시킬수 있음. 

`<track>`태그를 이용해 여러개의 자막을 제공해줄수도 있으며 `label` 속성을 통해 각각의 자막의 의도를 명확히 명시해줘야함.