# 그래픽
## 배경
- background-image는 기본적으로 그림을 반복적으로 삽입한다.  
이를 원하지 않으면 background-repeat: no-repeat 속성을 사용한다.  
- background-attatchment는 컨텐츠의 크기가 커져서 scroll이 발생했을 때, 어떻게 보여지느냐에 대한 옵션이다. 기본값은 scroll로, 함께 스크롤이 된다. fixed를 사용하면, 그림은 가만히 있도록 설정이 가능하다.  
- background-size는 직접 픽셀값을 넣어줄 수도 있고, 옵션을 줄 수도 있다. cover / contain 옵션이 대표적인데, cover는 background를 그릴 item의 전체를 커버할 수 있도록 이미지 크기가 조정이 된다. contain은 해당 item이 모든 이미지를 보여줄 수 있도록 크기를 조정한다. 따라서, contain을 하게 되면 item의 일부분이 빈것처럼 보여질 수 있다.
- background-position은 이미지 정렬을 어떻게 할 것인지 설정할 수 있다.
- 위의 모든 속정은 background 속성 안에 shorthand로 설정할 수 있다.

## filter
원본 이미지를 그대로 두고, 이미지에 다양한 효과를 주는 방법이다.  
이미지 뿐만 아니라, 지도나 영상, 심지어 text에도 적용할 수 있다. hover 등의 이벤트와 transition을 활용하여 다양한 효과를 발생시킬 수 있다.

## transform
Element의 크기 조정이나 회전, 비틀기 등을 할 수 있다.  
주의할 것은, element가 block level element 또는 inline-blck element일 때만 적용 가능 하다는 것이다.

## transition
css에서 여러 속성들에 대해, 그 변형을 부드럽게 하기 위한 속성이다. mouse hover 시, element가 한 번에 확 바뀌는것 보다, 서서히 바뀌는 것이 더 자연스럽다.  
transition-property는 어떤 항목에 대해 transition을 적용할 것인지를 일렬로 적는 공간이고, duration은 전환하는 시간이다.  
간단하게 transition이라는 shorthand로 사용도 가능하다.  
transition의 대상이 되는 각 항목의 duration을 다르게 사용하고 싶으면 아래와 같이 사용할 수도 있다.
``` css
a {
  transition: font-size 1s, transform 0.1s
}
a:activd {
  transform:translate(20px, 20px);
  font-size:2rem;
}
```

transition-delay는 전환 효과를 바로 주지 않고, 지연시키는 속성이다.  
transition-time은 ppt에서 날아오기 효과 옵션이라고 생각하면 쉬울 것 같다. 같은 속도로 변환되거나, 빨라졌다 느리게 변환되는 등의 트랜지션을 사용할 수 있게 한다.