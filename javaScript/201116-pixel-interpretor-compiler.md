# 픽셀

화면을 구성하는 가장 작은 단위로 일반적으론 빛의 3원색인 빨강 초록 파랑 (RGB)로 구성되어 있음. 
이미지 전체를 구성하는 <b>픽셀</b>의 수가 많을수록 더 디테일하고 선명한 표현이 가능 (해상도). 


애플이 레티나 디스플레이를 내놓으면서, 전통적인 픽셀의 개념이 하드웨어 픽셀과 소프트웨어 픽셀 두가지로 분리 됨. 하드웨어 픽셀은 기존에 우리가 알고 있던 그 픽셀(화면에서 점 하나)을 의미하고 CSS픽셀이라고도 불리는 소프트웨어 픽셀은 새롭게 생긴 하나의 단위이다.

하나의 "CSS 픽셀"은 화면 해상도에 관계없이 항상 "CSS 인치"의 1/96과 같은 반면 하드웨어 픽셀은 화면 해상도에 따라 상대적으로 크기가 변화 함	


# 컴파일러 언어 vs 인터프리터 언어



가장 큰 차이점은 실행 단계에서의 차이

 컴파일 언어는 코드를 분석하고 기계가 이해 할수있는 machine code를 실행전에 생성하는 ‘컴파일러’ 단계가 필요하고 인터프리터 언어는 별도의 ‘컴파일러’ 과정없이 한줄한줄 해석해서 바로 실행하는 언어. 

인터프리터 언어 같은 경우는 컴파일 과정이 별도로 필요하지 않고 과정이 단순하기 때문에 생산속도가 빠르지만 실행속도면에선 한번 생선된 파일에 의해 프로그램이 실행되는 컴파일 언어가 확실히 빠름. 
연산속도나 실행속도에 민감함 프로그램은 인터프리터 언어로 개발하지 않음.

또 인터프리터 같은 경우는 소스 코드가 실행되기 전까지는 소스 코드의 버그를 인지하는 것이 어렵기 때문에 인지시점이 컴파일러 언어에 비해 늦음.