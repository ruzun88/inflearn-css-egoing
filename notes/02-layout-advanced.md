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