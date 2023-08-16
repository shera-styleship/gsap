# GSAP
타임라인 기반의 애니메이션 자바스크립트 라이브러리<br>
[공식문서](https://greensock.com/docs/v3)


### 환경구성
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.4.2/gsap.min.js"><script>
```
[gsap 설치가이드](https://greensock.com/docs/v3/Installation)


### GSAP엔진을 이용해 제어할 수 있는 속성
- Create animations
- Configure settings
- Register plugins, eases, and effects
- Global control over all animations

Create animations 파트에서는 크게 Tweens 과 Timelines 두가지의 오브젝트를 가지고 있음.


### tweens
Tweens는 모든 애니메이션이 작동하는 역할을 말하며,  ( high-performance property setter  )
대상 ( 애니메이션을 적용할 객체) 에게 duration, animation-properties 정보를 입력하는 하나의 단위로 해석함.


### Common methods for creating a Tween
gsap.to()

```js
gsap.to('.elem',{duration:1,x:100,y:100,rotation:45});
```

gsap.from()

메서드는 지정한 값(위치)에서 부터 원래의 값(위치)으로 애니메이션 
```js
gsap.from('.orange',{x:400, y:400});
```

gsap.fromTo()
```js
gsap.fromTo(".orange", 
    {x:700, y:400, scale:1, opacity:0, duration:1},
    {x:400, y:200, scale:3, opacity:1, duration:3});
```
[예시](https://codepen.io/shera9961/pen/XWyLpEB)


### 지연 과 반복
- delay : 애니메이션이 시작되기 전에 지연시간을 지정.
- repeat : 애니메이션이 몇번 반복되어야 하는지를 지정.
- yoyo : `true` 로 설정하면 애니메이션이 앞뒤로 재생.
- repeatDelay : 각 반복 사이에 발생하는 지연시간을 지정.

! 무한 반복은 <u>repeat: -1</u> 을 설정하면 애니메이션이 무기한 반복

! yoyo 속성은 <u>repeat</u> 설정이 들어있어야 사용가능

[예시](https://codepen.io/shera9961/pen/ZEmNBxe)

```jsx
gsap.to(".orange", {x:300, repeat:-1, yoyo:true, repeatDelay:1});
```
### 가속도
ease는 애니메이션이 재생될 때의 변경 속도를 제어함.

[참고사이트](https://greensock.com/docs/v3/Eases?ref=6234)


### 다중요소 제어
stagger속성을 사용하면 단일 트윈에서 여러 대상의 시작 시간을 오프셋 설정할 수 있음.<br>
[예시](https://codepen.io/shera9961/pen/yLQmVjy)

```
from 으로 받을 수 있는 값

first, end, center, edges
```

```js
gsap.to(".stage .box", {y:-50, stagger:{
  each:0.2,
  from:"end"
  }
});
```
[예제사이트](https://codepen.io/shera9961/pen/vYQoyjRq)



### 트윈컨트롤

```
let tween = gsap.to('.orange', {x:500})

document.querySelector('.restart').addEventListener('click', ()=>{ tween.restart() })

tween.play();
tween.pause();
tween.resume();
tween.reverse();
tween.restart();
```

[예제사이트](https://codepen.io/kindtigerr/pen/poaMRJV?editors=1111)



### Timeline
타임라인 사용으로 복잡한 시퀀스의 애니메이션을 간단하게 만들 수 있음.



### 타임라인

타임라인은 gsap.timeline()으로 생성

```jsx
gsap.timeline()
  .from('.sun',{duration:1,opacity:0,x:50,y:50})
  .from('.gress',{duration:1,opacity:0,y:100,stagger:0.2})
  .from('.bird',{duration:1,opacity:0,y:100})
  .from('.music',{duration:1,opacity:0,x:100,y:100})


var tl = gsap.timeline();
tl.to(".green", {duration: 1, x: 200});
```
```
브라우저 성능을 고려 한다면 ..

브라우저 성능을 최대치로 끌어올리기 위해선 CSS Transform과 Opacity의 애니메이션을 사용하길권함.
CSS Transform 과  Opacity 가 아닌 값을 변경하면 브라우저가 페이지 레이아웃을 다시 랜더링(re-rander)하여 트윈이 많을 경우 성능을 저하시킬 수 있음.

대상의 크기만큼 이동할때에는 px말고 %로 이동하는게 좋다.
x: “100%”
`xPercent(100)   =  transform:translateX(100%)`

`yPercent(100)   =  transform:translateY(100%)`
```

[예제](https://codepen.io/shera9961/pen/vYQwybM)

```js
gsap.timeline()
  .from('.sun',{duration:1,opacity:0,x:50,y:50})
  .from('.gress',{duration:1,opacity:0,y:100,stagger:0.2})
  .from('.bird',{duration:1,opacity:0,y:100})
  .from('.music',{duration:1,opacity:0,x:100,y:100})
```


### Position Parameter 시각적 효과

타임라인 위치 매개변수 설정<br>
위치 매개변수를 사용하면 타임라인에서 트윈의 시작 시간을 오프셋 할 수 있다.


[예제](https://codepen.io/kindtigerr/pen/GRQVWmB)

```js
 const tl = gsap.timeline();
  tl.to(object, {y:300}, "+=1")  // 이전 트윈 종료 후 1초 뒤에 시작
  tl.to(object, {x:300}, "-=1")  // 이전 트윈 종료 1초 전에 시작
  tl.to(object, {rotation:90}, "<")  // 이전 트윈 시작될 때 동시에 실행
  tl.to(object, {opacity:0.5}, "<1") // 이전 트윈 시작 된 후 1초 뒤에 실행
  tl.to(object2, {x:200}, 1) // 타임라인 1초에 실행 
```


### 단일메뉴 효과
애니메이션 버튼이나 GSAP 의 다른요소에 인터렉션을 추가하는것은 CSS 애니메이션이랑 약간 다름.

CSS 는 기본 클래스에서 :hover 선택자를 이용해서 여기에 자연스러운 효과(정확한 타이밍이 필요한 여러 객체들을 컨트롤 하거나 재색, 되돌아가기, 속도,기속도 설정)를 주기위해서는
gsap의 애니메이션이 훨씬 더 많은 유연성이 있음.

GSAP를 사용해서 작업할때는 paused된 에니메이션 객체(tween or timeline)을 생성.
javascript의 mouse event를 사용해(mouseenter, mouseleave)애니메이션 객체에 play() 또는 
reverse()를 적용한다.

[예제](https://codepen.io/kindtigerr/pen/jOZgmJG)




