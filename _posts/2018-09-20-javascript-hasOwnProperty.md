<h1>hasOwnProperty</h1>
<h2>prototype chain</h2>
<p>javascript는 고전적인 상속모델이 없다. 다만 prototype을 사용한다.</p>
<p>javascript 상속은 프로토타입 체인을 사용한다는 것이다. </p>
<p>객성의 속성을 조회할 때 javascript는 상위 proto를 트래버스한다. 요청된 이름을 찾을때까지 위쪽을 탐색한다. 
체인의 최상위(object.prototype)에 도달하였는데도 아직 원하는 값을 얻지 못한 경우 'undefined'를 반환한다.</p>

<h2>hasOwnProperty</h2>
<p>객체가 자신의 자체적으로 정의 된 속성을 가지는지 확인하려면 Object.prototype에서 상속하는 hasOwnProperty 메소드를 사용해야한다.</p>
<p>hasOwnProperty는 프로토 타입 체인을 트래버스하지 않는 JavaScript 프로퍼티이다.</p>

<h2>for-in loop</h2>

```
Object.prototype.foo = 1;

var bar = {moo : 2};

for (var i in bar) {
    console.log (i); // foo와 moo를 모두 인쇄한다.
}

for (var i in bar) {
    if (foo.hasOwnProperty (i)) {
        console.log (i);
    }
}
```

<p>마지막 for-in문 코드에서hasOwnProperty가 자체 속성을 확인하기 때문에, 단지 moo를 출력 한다. 
hasOwnProperty가 생략되면 원시 프로토 타입이있는 경우 코드가 오류가 발생하기 쉽다.</p>
<p>최신 버전의 ECMAScript에서는 Enumerable이 아닌 속성을 Object.defineProperty로 정의하여 hasOwnProperty를 사용하지 않고 속성을 반복 할 위험을 줄인다. 
그럼에도 불구하고 새로운 ECMAScript 기능을 아직 사용하지 않는 Prototype과 같은 오래된 라이브러리를 사용할 때는주의해야한다. 
이 프레임 워크가 포함되면, hasOwnProperty를 사용하지 않는 in 루프는 중단 될 수 있다.</p>
<p>결론적으로
ECMAScript 3 이하에서는 물론 라이브러리 코드에서 항상 hasOwnProperty를 사용하는 것이 좋다. 
네이티브 프로토 타입이 확장되었는지 아닌지에 대한 이러한 환경에서는 가정을해서는 안된다. 
ECMAScript 5부터 Object.defineProperty를 사용하면 열거되지 않는 속성을 정의하고 응용 프로그램 코드에서 hasOwnProperty를 생략 할 수 있다.</p>
