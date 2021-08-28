# 레이아웃 기본
## inline vs 블록
h1은 블록, a태그는 인라인이다.  
블록태그에 border를 주면 화면 전체를 사용하는 것을 볼 수 있고,  
a태그에 border를 주면, 자기 크기만큼만 쓰는 것을 볼 수 있다.  
태그 별로 inline인지 block인지 정해져 있긴 하지만, css를 통해 얼마든지 바꿀 수 있다!  
``` cs
h1 {
  display: inline;
}
a {
  display: block;
}
```

## Box Model
가장 중요한 주제 중 하나이다.  
여백, 위치, 크기 등을 결정하는 것이 box 모델이다.  
- padding: 박스 크기 안쪽으로의 여백
- margin: 박스 크기 바깥쪽으로의 여백

통상적으로 block level element는 화면 전체를 사용한다. 싫다면, width값을 사용하면 된다. 높이도 지정할 수 있다.

### inline level에서의 box model
block level과 다르게 동작한다.  
margin과 padding은 정상적으로 적용이 된다.  
하지만, width, height 값은 적용되지 않는다.

## Box Sizing
element의 padding, border 등의 값을 할당할 때, 예상한 크기와 다르게 나올 때가 있다.  
css의 element의 크기는 content 영역의 크기를 width로 지정한다. border는 컨텐츠 외부에 그려지는 것이므로, border 두께를 두껍게 하면, 그만큼 보여지는 크기는 더 커지게 된다.  
이를 원하지 않는다면, box-sizing 옵션을 활용하여 수정할 수 있다.  
선택 가능한 것은 border-box, content-box 등이 있다.  
default 값은 컨텐츠 영역의 사이즈, 즉 content box이다.  
border-box를 선택하면, 내부의 content 사이즈를 줄여서 결과적 크기를 맞춘다.  
UI 특성상, 보여지는 크기가 중요하므로, 모든 content에 대해 box-sizing을 border-box로 하는 것이 권장되기도 한다.
``` css
* {
  box-sizing: border-box;
}
```

## margin 겹침 (고급 과정)
어떨때 margin이 사라지는 경우가 있다.
### 1번 case
h1 태그를 연속적으로 사용했을 때, 마진이 겹쳐버리는 경우가 발생한다.  
위에 있는 component(이하 A)와 아래 있는 component(B)의 마진 값 중 더 큰 값만 적용이 되어 버린다.
그래서 A 마진을 100px, B의 마진을 150px을 할당하면, 250px의 간격이 생기는 것이 아니라, B의 마진인 150px만 발생하게 된다.  
즉, 
- A.margin + B.margin 이 아니라,
- max(A.margin, B.margin)이 적용된다.

### 2번 Case
부모 element(A) 아래에 자식 element(B)가 있고, 두 element 모두 margin이 있는 경우 발생할 수 있다.
parent의 size와 관련된 시각적인 효과가 사라지는 경우에 마진 겹침 현상이 발생한다.  
parent에 border가 있으면, 정확한 사이즈와 위치를 알 수 있다. 이때는 마진 겹침이 일어나지 않는다.  
그런데, border를 없애는 순간, 마진이 겹쳐버린다!  
적용되는 마진값:
- max(A.margin, B.margin)

### 3번 Case
동등한 Level의 두 element A, B가 있다. 시각적인 효과가 없으면, 마진 겹침이 일어난다. A는 빈 element, B에는 유효한 element가 있으면, A와 B사이에는 마진 겹침이 일어난다는 것이다.  
앞의 case와 동일하게 큰 마진값을 택하게 된다.

## position - relative, static
element는 left, right, top, bottom 등의 키워드로 위치를 지정할 수 있다.  
하지만, position 값을 지정하지 않으면, left/top 등의 값을 바꾸어도 element의 위치가 변경되지 않는다.  
position의 default 값은 static인데, 이를 relative로 바꾸어야 위치 변경 키워드가 동작한다.  
static은 left/top 등의 offset값을 무시하고, 자기가 있어야 할 고정적 위치를 지키고 있는 옵션이다.

## position - absolute
absolute는 절대 위치를 의미한다.  
relative는 부모 tag에 대한 위치이지만, absolute는 html 문서 전체에 대한 절대적 위치이다.  
### 주의할 점
1. 부모-자식 관계의 영향도 감소
    - position에 absolute를 설정하고, left나 top값을 주지 않는다면, 부모의 위치 바로 아래가 자신의 absolute 위치가 된다는 것이다. 왜냐하면 left, top 값의 default값이 0이 아니라, 본인이 있기로 기대되는 장소의 값이기 때문이다.
    - 또한, position이 absolute가 되는 순간, 부모 element와의 관계가 소원(?)해진다. 그래서 부모 element의 영역 안에는 자식 element의 공간이 없게 되어, 박스 사이즈도 마치 자식 element가 없는 것 처럼 보이게 된다.
    - 자식 element 또한, 부모의 size를 inherit받지 않고 자기 content만큼의 박스만 가지게 된다. 따라서, 자식 element의 크기를 지정해주고 싶다면, 자식 element에 직접 값을 할당해주어야 한다.
1. 부모의 position이 relative일 때
    - 부모의 position이 static이고, 자식의 position이 absolute라면, 문서 전체 기준으로 element의 offset값이 적용된다.
    - 부모의 position이 relative이고, 자식의 position이 absolute라면, 부모의 위치를 기준으로 element의 offset값이 적용된다.
1. 부모의 position은 지정된 값이 없는 경우
    - 부모의 position이 지정된 값이 없다는 것은 default값인 static이라는 것이다.
    - position이 absolute인 자식 element는 static은 조상 element는 모두 무시하기 때문에, 계속 윗 세대로 가면서 position이 static이 아닌 값이 있을때까지 position값을 탐색한다.
    - static이 아닌 조상이 발견되면, 그것을 기준으로 자신의 위치를 결정한다.

## position-fixed
fixed는 absolute와 비슷한 동작은 하는것 처럼 보일 수 있다. 페이지의 세로 높이가 한페이지를 넘어가지 않는다면, 동일한 동작을 할 수 있다.  
그러나 페이지 크기가 커서 스크롤이 발생하게 되었을 때, fixed는 스크롤을 하더라도, 고정된 위치에 있게 된다.  
width와 height값을 지정하지 않는다면, 부모 element와 관계 없이, 딱 자기 크기만큼의 박스만 가지게 된다.