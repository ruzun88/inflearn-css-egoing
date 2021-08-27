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