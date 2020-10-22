## Animation


오늘은 animation을 사용해 간단한 애니메이션을 넣어보는 시간을 가졌다. 개인적으로 많이 부족하다고 생각한 부분이였는데 이번 강의를 통해 조금 보충할수 있었던 거 같다. 물론 오늘 이후로 계속 더 써보며 익숙해져아겠지만 이론적인 부분은 여기에 간략하게 써가며 정리해보겠다.

- 일단 css animation을 사용하면 별도의 스크립트 없이도 간단하게 애니메이션을 만들수 있음
- 스크립트로 더 정교한 애니메이션을 만들수 있을진 몰라도 성능면에선 css animation이 우위. css 애니메이션도 어떤 방법을 쓰느냐에 따라 성능이 다를수 있음. 예를 들어 어느 요소를 움직여야 할때 translate, padding, margin, position 등으로 움직이는 애니메이션을 줄 수 있는데 translate가 성능면에서 뛰어난편이라 주로 쓰이는 편이라고한다.


animation도 단일속성과 속기형으로 작성이 가능한데 주로 속기형으로 작성해서 단일속성의 정확한 명칭을 잘 모르고 있었다. 자주 쓰이는 속성을 정리해보면 

    animation-name: 애니메이션 이름 정의
    animation-duration: 한 싸이클의 애니메이션이 얼마에 걸쳐 일어날지 지정
    animation-delay:로드되고 나서 언제 애니메이션이 시작될지 지정. 한번에 다 같이 시작하면 이상할수 있으니 요소마다 delay를 다르게 줘서 순차적인 애니메이션 구현 가능
    animation-direction: 애니메이션 종료후 다시 처음부터 시작할지 역뱡향으로 시작할지 지정. normal, reverse, alternate
	animation-iteration-count 애니메이션을 몇번 반복할지 지정. 원하는 수치 입력하거나`infinite` 로 지정해 무한 반복가능
	animation-fill-mode: 시작전이나 후 어떤 값이 적용될지 지정
	animation-play-state: 애니메이션 상태 설정 (paused, running)
	animation-timing-function: 애니메이션 효과의 시간당 속도 (linear, ease-in, ease-out)

 

애니메이션을 사용하기 위해 애니메이션을 정의해줘야하는데 이때 `@keyframes`를 사용. 만약 fadeOut이라는 애니메이션을 만든다고하면 아래와 같이 작성

```css
@keyframes fadeOut {
	0% {
	opacity: 1;
	}
	100% {
	opacity: 0;
	}
}
```
또는 


```css
@keyframes fadeOut {
	from {
	opacity: 1;
	}
	to {
	opacity: 0;
	}
}
```

종합해보면 `.ball` 클래스에 fadOut 애니메이션을 적용해 1초 지연시간후 2초동안 사라지고 나타나고를 무한반복하는 애니메이션을 아래와 같이 작성하여 만들수 있다. 

```css
	.ball{
		animation-name: fadeOut;
		animation-duration: 2000ms;
		animation-delay: 1000ms;
		animation-iteration-count: infinite;
		animation-timing-function: ease-in-out;
		animation-direction: alternate;
	}
```

속기형으로 작성시 `name` , `duration` 은 필수로 써주고 그 다음 속성은 순서와 상관없이 나열 해주면 됨
```
animation: fadeOut 2000ms 1000ms infinite linear alternate;
```


