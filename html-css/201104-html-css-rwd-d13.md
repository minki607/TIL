### 반응형 웹디자인 (Responsive Web Design)

##### label ≠ placeholder

반응형 디자인 설계시 모바일 뷰포트에 label을 삽입할 공간이없어 label을 생략하고 placeholder를 대신 사용하는 경우가 종종 있음. 

하지만 이 두 속성의 용도는 많이 다르기 때문에 둘다 제공하되, label이 너비를 차지하지 않도록 디자인하는 floating label 방법을 채택할수 있음 

![floating-label](https://cdn.dribbble.com/users/72481/screenshots/1933559/jupiturf3.gif)
출처: https://dribbble.com/shots/1933559-Jupiturf-Floating-Label-Form/attachments/1933559-Jupiturf-Floating-Label-Form?mode=media



처음에는 label을 placeholder자리에 `position:absolute`로 위치시켜주고 focus를 받게되면(is--focus 클래스를 가지면) input요소 상단부분에 위치시켜주면 너비를 차지 하지 않고도 활용가능함.

```css
.member-id, member-password {
  position: relative;
}
.member-id label, .member-password label {
  position: absolute;
  left: 0.5em;
  top: 15px;
  font-size: 1.8rem;
  transition: all 0.2s;
}

.is--focus label,
 {
  font-size: 1.3rem;
  transform: translate(-0.5em, -15px);
}
```

##### checkbox 커스텀 디자인 설정하기

checkbox의 경우 직접 스타일을 변경해줄순 없지만 기존의 checkbox를 숨기고 새로운 디자인 (배경이 적용된) input 모양의 요소로 대체해줄수 있음.

아래 예제에서는 checkbox 클래스를 가진 span이 이 역활을 해줌.

```html
<div class="save-email">
  <input type="checkbox" id="userEmailSave" />
  <span class="checkbox"></span>
  <label for="userEmailSave">이메일 저장</label>
</div>
```

체크박스 span이 input뒤에 마크업된 이유는 + 또는 ~ 선택자를 사용해 input이 체크 되었을때 뒤에오는 형제 요소를 선택하기 위함.

css 특성상 전에 마크업된 요소들을 선택할수 있는 선택자가 없기 때문에 이런 마크업 구조를 선택함.

```css
.save-email .checkbox{
  position: absolute;
  width: 16px;
  height: 16px;
  top: 50%; 
  left: 0;
  transform: translateY(-50%); /*정중앙에 위치 시킴*/
  background: url(../images/icon-un-checked-square.svg) no-repeat 0 0;
}

  /*input이 체크되었을때 형제요소인 체크박스를 선택*/
.save-email input:checked + .checkbox {

  background-image: url(../images/icon-checked-square.svg);
}
```


