### 반응형 웹디자인 (Responsive Web Design)

![responsive patterns](https://image.slidesharecdn.com/mobiledesignstrategicsolutions-120823190643-phpapp02/95/mobile-design-strategic-solutions-55-728.jpg?cb=1345800663)

#### 여러 디자인 패턴중 상황에 맞게 설계

**Flexible vs Adaptive**

Flexible - 유연하게 레이아웃이 바뀌게 하기. 좀 더 세밀한 설계가 필요.
Adaptive - 디바이스에 맞게 레이아웃 자체 크기를 바꿈

- Mostly Fluid
  - 모바일 환경에 맞춰 레이아웃을 설계한뒤 뷰포트에 따라 레이아웃 확장. 큰 스크린에서는 열과 열사이에 margin이 있고 스크린이 작아질수록 컨텐츠가 하나의 열에 쌓이는 형식.
- Column Drop
  - 뷰포트가 작아질때마다 열 하나를 내리는 방식.
- Layout Shift 
  - 디바이스 사이즈에 따라 레이아웃 구조를 바꾸는 방법.
- Tiny Tweaks
  - 뷰포트에 따라 조금씩 변형
- Off Campus 
  - 여러단의 레이아웃을 뷰포트에 맞게 1,2,3단에 맞춰 보이게 함.

#### 설계시에는 모바일 먼저 데스크탑 나중

모바일 환경의 레이아웃을 먼저 구현하는게 더 쉽고 성능정인 측면에서도 훨씬 우수할수 있음. 데스크탑에 필요한 기능들만 하나씩 추가하며 불필요한 미디어쿼리를 최소화 하는 방법이 젤 효과적임. 현업에서는 데스크탑 버전을 모바일로 구현하는 작업을 많이하고 있으며 이는 더 구체적인 설계가 필요함.

#### 미디어 쿼리를 사용해 디바이스 레이아웃 설계
화면 크기가 768px 보다 큰 디바이스(데스크탑):
```css
@media all and (min-width:768px) {화면 크기가 최소 768px 이상일때 이 안에 명시된 css가 적용됨}
```

화면 크기가 576px 보다 작은 디바이스(모바일):
```css
@media all and (min-width: 576px) { 최대 화면 크기가 576px일때 이 안에 명시된 css가 적용됨 }
```

- all 대신 , screen 또는 print를써 구체적으로 무슨 용도로 사용될껀지 명시해주면 그에 따라 효과적으로 스타일링이 적용됨.



768px, 576px이런 화면 디바이스 breakpoint 크기는 [Media Query Breakpoint](http://devfacts.com/media-queries-breakpoints-2020/)  참조. 프로젝트 타겟에 맞춰 breakpoint도 유동적으로 선택해주면 됨.

#### 반응형 디자인에서 이미지 처리하기

```css
img{
  max-width: 100%;
  height: auto;
}
```
- img가 부모요소에 의해 원본의 크키보다 더늘어날수도 있기에 `max-width: 100%` 설정을해줘 원본의 100%를 유지하도록함.

- height값은 auto를 줘서 자동으로 비율을 유지하면서 늘어날수 있도록 해줌.

- 이미지 크기와 관련한 성능/속도 문제

  - 이미지 최적화를 해주면 성능또한 높힐수 있기 때문에 상황별 최적화된 이미지 확장자를 사용하고 포맷 특성도 고려하며 저장. [자세한 내용](https://medium.com/guleum/%EC%84%BC%EC%8A%A4%EC%9E%88%EB%8A%94-%EB%94%94%EC%9E%90%EC%9D%B4%EB%84%88%EA%B0%80-%EB%90%98%EA%B8%B0%EC%9C%84%ED%95%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EC%B5%9C%EC%A0%81%ED%99%94-161c3b3212cc)은 이 포스트 참조. 

- 아트 디렉션 처리 
   - 큰 화면에서만 잘 보이고 작은 화면에서는 잘 안보일수 있는 이미지를 적당히 잘라 (crop) 필요한 부분만을 사용해 의미전달을 할 필요가있음

각각의 뷰에 따라 적절한 용량의 이미지를 지정해주는 방법

picture태그안에 source태그의 srcset속성을 사용하기. IE에서는 이 속성을 지원하지 않아 fallback 이미지를 반드시 같이 넣어줘야함.

```html
<picture>
    <source srcset="/media/cc0-images/surfer-240-200.jpg"
            media="(min-width: 800px)">
    <img src="/media/cc0-images/painted-hand-298-332.jpg" alt="" /> 필수!!
</picture>
```

img태그의  srcset을 사용하기

```html
<img srcset="elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 600px) 480px,
            800px"
     src="elva-fairy-800w.jpg"
     alt="Elva dressed as a fairy">

```
