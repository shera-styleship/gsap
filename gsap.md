# GSAP
타임라인 기반의 애니메이션 자바스크립트 라이브러리

<br>

## GSAP엔진을 이용해 제어할 수 있는 속성
- Create animations
- Configure settings
- Register plugins, eases, and effects
- Global control over all animations



### Common methods for creating a Tween

gsap.to()

```
gsap.to('.elem',{duration:1,x:100,y:100,rotation:45});
```

gsap.from()

메서드는 지정한 값(위치)에서 부터 원래의 값(위치)으로 애니메이션 
```
gsap.from('.orange',{x:400, y:400});
```

gsap.fromTo()
```
gsap.fromTo(".orange", 
    {x:700, y:400, scale:1, opacity:0, duration:1},
	{x:400, y:200, scale:3, opacity:1, duration:3});
```
[예시](https://codepen.io/GreenSock/pen/wvwEOZL)


### Staggers 
  개체의 애니메이션의 시작 사이에 약간의 지연시간을 넣어 보다 쉽게 제어 가능
[예시](https://codepen.io/GreenSock/pen/RwbZaZK)

### Timeline
타임라인 사용으로 복잡한 시퀀스의 애니메이션을 간단하게 만들 수 있음.

```
var tl = gsap.timeline();


tl.to(".green", {duration: 1, x: 200});
tl.to(".orange", {duration: 1, x: 200, scale: 0.2});
tl.to(".grey", {duration: 1, x: 200, scale: 2, y: 20});

```

```
브라우저 성능을 고려 한다면 ..

브라우저 성능을 최대치로 끌어올리기 위해선 CSS Transform과 Opacity의 애니메이션을 사용하길권함.
CSS Transform 과  Opacity 가 아닌 값을 변경하면 브라우저가 페이지 레이아웃을 다시 랜더링(re-rander)하여 트윈이 많을 경우 성능을 저하시킬 수 있음.
```

### 지연 과 반복
- delay : 애니메이션이 시작되기 전에 지연시간을 지정.
- repeat : 애니메이션이 몇번 반복되어야 하는지를 지정.
- yoyo : `true` 로 설정하면 애니메이션이 앞뒤로 재생.
- repeatDelay : 각 반복 사이에 발생하는 지연시간을 지정.

! 무한 반복은 <u>repeat: -1</u> 을 설정하면 애니메이션이 무기한 반복

! yoyo 속성은 <u>repeat</u> 설정이 들어있어야 사용가능


### 가속도
ease는 애니메이션이 재생될 때의 변경 속도를 제어함.

[참고사이트](https://greensock.com/docs/v3/Eases?ref=6234)


### 다중요소 제어
stagger속성을 사용하면 단일 트윈에서 여러 대상의 시작 시간을 오프셋 설정할 수 있음.

```
gsap.to(".stage .box", {y:-50, stagger:{
  each:0.2,
  from:"end"
  }
});
```
[예제사이트](https://codepen.io/kindtigerr/pen/bGLXBzq)


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

### 타임라인
타임라인은 gsap.timeline()으로 생성


```
gsap.timeline()
  .from('.sun',{duration:1,opacity:0,x:50,y:50})
  .from('.gress',{duration:1,opacity:0,y:100,stagger:0.2})
  .from('.bird',{duration:1,opacity:0,y:100})
  .from('.music',{duration:1,opacity:0,x:100,y:100})

```




