<h1>자바스크립트 실행 컨텍스트</h1>
<h2>실행 컨텍스트의 종류</h2>
<p>1. 전역 실행 컨텍스트: 기본 실행 컨텍스트이며 어떤 함수에도 포함된지 않는 코드들이 이곳에 저장된다. 브라우저일때 window object에 global object를 만든다. 그리고 'this'의 값을 global object와 같게 설정한다. 프로그램 내에서 오직 한가지의 전역 실행 컨텍스트만 존재한다.</p>
<p>2. 함수 실행 컨텍스트: 함수가 호출되고 실행될 때마다 생성되는 실행컨텍스트이다. 또한 함수가 호출될 떄마다 실행 스택에 새로 만들어지는 스택이 쌓인다. 따라서 여러가지 함수 실행 컨텍스트가 존재할 수 있다.</p>
<p>3. eval 함수 실행 컨텍스트: eval 함수 내에도 실행컨텍스트가 존재한다. 하지만 javascript 개발자들이 잘 다루지는 않는다.</p>

<h2>실행 스택(execution stack, calling stack)</h2>
<p>LIFO(last in first out)구조를 가지며 코드가 실행될 동안 실행스택이 발생할 때마다 이곳에 스택이 쌓이게 된다.</p>
<p>자바스크립트 엔진이 처음 코드를 발견하면 전역 실행 컨텍스트가 현재 실행 스택에 쌓인다. 그리고 새로운 함수 실행 컨텍스트가 호출될때마다 새로운 컨텍스트가 실행 스택에 쌓이게 된다.</p>
<p>자바스크립트 엔진은 실행 스택의 가장 높은 레벨에 있는 실행 컨텍스트를 실행시킨다. 그리고 실행이 완료되면 그 컨텍스트는 사라지고 현재 실행스택에서 최상위에 존재하는 실행 컨텍스트가 실행된다.</p>

~~~
let a = 'Hello world';

function foo(){
  console.log('first foo function execution context');
  bar();
  console.log('second foo function execution context');
}

function bar(){
  console.log('bar function execution context');
}

console.log('first global execution context');
foo();
console.log('last global execution context');
~~~

<p>위 코드에서 콘솔로그에 의해 찍히는 텍스트들이 실행 컨텍스트가 실행되고 종료되기까지의 순서를 나타낸다.</p>
<p>처음 'first global execution context'가 생성될 때 전역 실행 컨텍스트가 생성된다.</p>
<p>이후 'first foo function execution context'가 실행될 때 첫번째 함수 실행스택인 foo functional Execution Stack이 현재 실행 스택에 쌓인다.</p>
<p>'bar function execution context'가 콘솔에 찍히는 순간 실행스택에서 bar 실행 컨텍스트는 foo 실행 컨텍스트의 위에 쌓이고 실행이 되는 순간 실행 스택에서 팝오프된다.</p>
<p>'second foo function execution context'가 찍히는 순간 bar 실행 컨텍스트는 이미 사라지고 자바스크립트 엔진 컨트롤이 foo functional execution context를 다시 가리키게 된다. 이 컨텍스트 역시 실행이 되고 실행 스택에서 팝오프된다.</p>
<p>'last global execution context'가 실행되는 순간이 맨 처음 생성되었던 전역 컨텍스트를 자바스크립트 엔진 컨트롤이 가리키게 되고 전역 실행 컨텍스트까지 팝오프 되며 실행 스택이 모두 비워지게 된다.</p>

<h2>실행 컨텍스트가 만들어지는 단계</h2>
<h3>1. 생성단계</h3>
<h4>  1) this binding: this의 값을 설정한다.</h4>
<h4>  2) LexicalEnvironment component가 만들어진다.</h4>
<h4>  3) VariableEnvironment component가 만들어진다.</h4>

~~~
ExecutionContext = {
  ThisBinding = <this value>,
  LexicalEnvironment = { ... },
  VariableEnvironment = { ... },
}
~~~

<h3>This Binding</h3>
<h4>전역 실행 컨텍스트: 'this'의 값은 global object를 가리키며 브라우저에서는 window object를 가리킨다.</h4>
<h4>함수 실행 컨텍스트: 함수가 어떻게 호출되었는지에 따라 'this'의 값이 결정된다. 객체 참조에 의해 함수가 호출된다면 'this'의 값은 그 객체를 가리키고 그렇지 않다면 global object를 가리키거나 엄격모드의 경우에는 'undefined'로 나타나게 된다.</h4>

<h3>LexicalEnvironment</h3>
<h4>identifier-variable mapping의 구조이다. 'identifier'은 변수와 함수의 이름을 말하고 'variable'은 함수를 포함한 실제 객체와 primitive value를 말한다.</h4>
<h4>LexicalEnvironment는 environment record와  reference to the outer environment로 나뉜다. 'environment record'는 변수와 함수가 실제 저장되는 장소이고 'reference to the outer environment'는 외부 환경에 접근할 수 있는 권한을 의미한다.</h4>

<h3>LexicalEnvironment의 두가지 타입</h3>
<h4>전역 실행 컨텍스트의 환경에서 Lexical Environment는 접근할 수 있는 외부 환경이 존재하지 않는다. 전역 환경의 'reference to the outer environment'는 'null'이다. 'environment record'에는 전역 객체(윈도우 객체)와 관련 메소드 및 속성(예, 배열 array) 사용자가 정의한 전역 메소드가 있다. 이 값들은 전역 객체를 참조한다. </h4>
<h4>함수 실행 컨텍스트의 환경에서 사용자가 함수 내에서 정의한 변수 및 함수들이 'environment record'에 기록된다. 'reference to the outer environment'는 전역 환경, 해당 함수를 감싸고 있는 외부 함수이다.</h4>
<h4>함수 환경 레코드에는 함수에 전달된 인덱스와 인수 사이의 맵핑, 인수의 길이가 저장된 arguments 객체도 포함된다.</h4>

<h3>environment record의 두가지 타입</h3>
<h4>선언적 환경 레코드는 변수, 함수, 파라미터들이 쌓인다.</h4>
<h4>객체 환경 레코드에는 전역 실행 컨텍스트에 나타난 변수와 함수의 연관성을 정의하는데 사용된다.</h4>

<h3>VariableEnvironment</h3>
<h4>실행 컨텍스트의 VariableStatements에서 생성된 바인딩을 'environment record'가 저장한다.</h4>
<h4>이 변수 환경은 어휘 환경이기도 한다. 그래서 어휘 환경에 정의된 요소들 모두를 포함한다.</h4>
<h4>ES6에서 나타난 LexicalEnvironment과의 차이점이 있다. LexicalEnvironment은 함수 선언과 'let','const' 바인딩을 저장하지만 VariableEnvironment는 'var' 바인딩만을 저장한다.</h4>

<h3>2. 실행단계</h3>
<h4>모든 변수에 대한 할당이 완료되고 코드가 최종적으로 실행된다.</h4>
<h4>실행 단계에서 JavaScript 엔진이 let 변수의 값을 소스 코드에서 선언 된 실제 위치에서 찾지 못하면 정의되지 않은 값을 할당합니다.</h4>

