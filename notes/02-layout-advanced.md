# 레이아웃 활용
## flex
레이아웃을 잡을 때 사용하는 개념 중 하나이다.  
flex를 사용하기 위해서는 부모에 해당하는 container와 그 안에 있는 item이 존재하여야 한다.  
각각이 사용할 수 있는 속성은 아래와 같다.  
|container|item|
|:-:|:-|
|display|order|
|flex-direction|flex-grow|
|flex-wrap|flex-shrink|
|flex-flow|flex-basis|
|justify-content|flex|
|align-items|align-self|
|align-content||

flex를 사용하기 위해서는 부모에게 display:flex를 할당해주어야 한다. 만약 이 선언이 되지 않으면, 원래의 속성을 유지하고, flex를 주게 되면 무언가 다른 행동을 하게 된다. (많고 복잡하고 까다롭다.)  

- block element를 가로로 정렬 : row(default) / row-reverse
- block element를 세로로 정렬 : column / column-reverse

div를 column / column-reverse 정렬하면, flex를 쓰지 않은 것과 동일하게 보일 수 있다. 하지만, height 값을 할당하면 달라진 것을 볼 수 있다. column일 때는 동일하지만, column-reverse를 하게 되면, container element의 하단에서부터 정렬이 되는 것을 볼 수 있다.

## flex의 속성 (grow, shrink)
grow와 shrink는 내부 item에 부여할 수 있는 속성이다.  
**flex-grow**는 상위 container의 공간 전체를 균등분배할 것인지에 대한 속성이다. 기본값은 0으로, 공간 전체에 대한 균등분배를 하지 않는다. 1이 되는 순간, 공간 분할을 한다.  
만약 2번째 항목에만 더 큰 공간을 할당하기 원한다면, nth-child값의 flex-grow값을 별도로 할당하여 변경할 수 있다.  
만약 다른 item은 0을 가지고, 한 항목만 1을 가진다면, 다른 item들은 여백을 가지지 않는다.  
**flex-basis**는 크기를 지정하는 속성이다.  
grow값의 지정 없이, flex-basis 값에 크기를 지정해 주면, 일반적인 경우에는 지정한 값이 그대로 화면에 나타난다. 하지만, 화면의 크기가 줄어들어 모든 항목을 담을 수 없게 되면, flex-basis를 할당한 item의 크기가 줄어들어 한 화면 안에서 모든 item을 볼 수 있게 된다.  
**flex-shrink**는 화면의 크기가 줄어들더라도 item의 크기를 그대로 유지할 수 있게 하는 속성이다. 즉, 다른 item이 화면에서 안보일 수도 있게 되는 것이다.  
이 기능을 원한다면, flex-shrink의 값을 0으로 주어야 한다.  
크기 손해를 보지 않겠다는 값이 0이라면, 그 이상의 숫자는 해당 item에 크기 손해를 감수한다. 하나의 item인 경우에는 모든 숫자에 대해 동일한 동작을 하겠지만, 두개 이상의 item일 때는 flex-shrink의 숫자 비율에 따라, 사이즈를 줄이는 폭이 달라진다.

## holy grail layout
holy grail layout은 header와 footer를 상하단에 가지며, 가운데 컨텐츠에는 navi, main, ad가 있는 형태를 의미한다.

## flex의 여러 속성들
(강의자료 보기)[https://opentutorials.org/module/2367/13526]
### container에 부여하는 속성
- flex-direction : item들의 정렬 방향 (기본값은 row)
- flex-wrap : 컨텐츠의 크기에 따라 자동으로 줄 바꿈(기본값은 nowrap)
- align-items: item의 높이 값을 정하는 방법 (기본값은 stretch, 컨테이너의 높이만큼 모두 커지게 만듦)
- justify-content: 수평과 관련된 속성 (direction이 row일 때.)
- align-content: align-items와 비슷함. align-items는 컨텐츠 전체를 움직이는 속성이라 하면, align-content는 한 줄에 있는 item을 하나의 그룹으로 묶고, 그 그룹을 정렬하는 방법을 나타낸다.

### item에 부여하는 속성
- align-self: 하나의 항목에 대해서만 다른 정렬을 하고 싶을 때 사용
- flex: flex-grow, flex-shrink, flex-basis를 축약한 속성
- order: item의 순서를 바꾸고 싶을 때 사용

## float
본문에 이미지를 삽입하는데 가장 많이 사용됨  
이미지의 경우, block content라서 row 전체를 먹고 있음. 하지만, float: left 속성을 할당해주면, 이미지는 왼쪽에 떠 있고, 그 다음 item들이 img 옆 남는 공간에 배치가 되기 시작함. 심지어 하나의 item으로 img의 폭이 다 차지 않는다면, 그 다음 item도 남는 옆 공간에 배치가 됨  
만약 이를 원하지 않는다면, style값에 clear:both;를 할당해 주면 됨

## multi column
신문처럼, 여러개의 column으로 나타낸 모양이다.  
column을 나타내는 방법은 여러가지다.  
- column-count : 단의 수를 강제로 지정, 폭은 자율에 맡김
- column-width : 단의 폭을 지정하여, 수는 자동으로 자율에 맡김
- 두 가지 다 사용 : width를 되도록 지키되, 최대 column-count개수만큼만 생성됨