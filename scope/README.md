# 스코프(Scope)  
스코프(Scope, 유효범위)는 자바스크립트를 포함한 모든 프로그래밍의 기본적인 개념입니다.  
<pre>
<code>
var  x = 'Global Scope';

function foo(){
    var x = 'function Scope';
    console.log(x);
}

foo();
//function Scope;

x;
//Global Scope
</code>
</pre>  

이름이 같은 변수 x가 중복 선언되었습니다. 전역에서 변수 x를 참조할 때, 그리고 함수 foo 내부에서 변수 x를 참조할 때 이름이 중복된 2개의 변수 중 어떤 변수를 참조해야 할까요? 자바스크립트는 어떻게 변수를 식별할까요?  
  

**스코프는 참조 대상 식별자  
(identifier, 변수, 함수의 이름과 같이 어떤 대상을 다른 대상과 구분하여 식별할 수 있는 유일한 이름)를 찾아내기 위한 규칙입니다. 자바스크립트는 이 규칙대로 식별자를 찾습니다.**  
  
# 스코프의 구분 
자바스크립트에서 스코프를 구분해보면 다음과 같이 2가지로 나눌 수 있습니다.  
```
전역 스코프(Global Scope)
코드 어디에서든 참조할 수 있다.
```
```
지역 스코프(Local scope or Function-level scope)  
함수 코드 블록이 만든 스코프로 함수 자신과 하위 함수에서만 참조할 수 있다.
```
  
모든 변수는 스코프를 갖습니다.  
변수의 관점에서 스코프를 구분하면 2가지로 나눌 수 있습니다. 
```
전역 변수 (Global variable)  
전역에서 선언된 변수이며 어디에든 참조할 수 있다.
```
```
지역 변수 (Local variable)  
지역(함수) 내에서 선언된 변수이며 그 지역과 그 지역의 하부 지역에서만 참조할 수 있다.
```
변수는 선언 위치(전역 또는 지역)에 의해 스코프를 가지게 됩니다.  
즉, 전역에서 선언된 변수는 전역 스코프를 갖는 전역 변수이고, 지역(자바스크립트의 경우 함수 내부)에서 선언된 변수는 지역 스코프를 갖는 지역 변수가 됩니다.  
  
전역 스코프를 갖는 전역 변수는 전역(코드 어디서든지)에서 참조할 수 있다. 지역(함수 내부)에서 선언된 지역 변수는 그 지역과 그 지역의 하부 지역에서만 참조할 수 있습니다.

  
# 자바스크립트 스코프의 특징  
자바스크립트의 스코프는 타 언어와는 다른 특징을 가지고 있습니다.  
  
자바스크립트는 **함수 레벨 스코프**(function level scope)를 따릅니다.  
함수 레벨 스코프란 함수 코드 블록 내에서 선언된 변수는 함수 코드 블록 내에서만 유효하고 함수 외부에서는 유효하지 않다(참조할 수 없다)는 것입니다.
  
단, ECMAScript 6에서 도입된 let keyword를 사용하면 블록 레벨 스코프를 사용할 수 있습니다.

<pre>
<code>
//자바스크립트는 함수 레벨 스코프를 따른다.
//블록 레벨 스코프를 따르지 않는다.
//그래서 1, 1이 결과로 출력된다.
var x = 0;
{
    var x = 1;
    console.log(x);
}
console.log(x);
</code>
</pre>
>1  
 1  
<pre>
<code>
//ECMAScript6의 let 키워드를 사용하면 블록 레벨 스코프를 사용할 수 있다.
let y = 0;
{
    let y = 1;
    console.log(y);
}
console.log(y);
</code>
</pre>
>1  
 0

# 전역 스코프(Global Scope)
전역에 변수를 선언하면 이 변수는 어디서든지 참조할 수 있는 전역 스코프를 갖는 전역 변수가 됩니다.
var 키워드로 선언한 전역 번수는 **전역 객체(Global Object) Window**의 프로퍼티입니다. 
<pre>
<code>
var global = 'Global';

function foo(){
    var local = 'Local';
    console.log(global);
    console.log(local);
}

foo();
//Global
//Local

console.log(global);
//Global

console.log(local);
//Uncaught ReferenceError: local is not defined
//함수 스코프 레벨의 변수이기 때문에 참조할 수 없다.
</code>
</pre>  

변수 global는 함수 영역 밖의 전역에서 선언되었습니다.   
자바스크립트는 타 언어와는 달리 특별한 시작점(Entry point)이 없어서  
위 코드와 같이 전역에 변수나 함수를 선언하기 쉽습니다.  

전역 변수의 사용은 변수 이름이 중복될 수 있고,  
**의도치 않은 재할당에 의한 상태 변화로 코드를 예측하기 어렵게 만드므로 사용을 지양해야합니다.**
  

# 비 블록 스코프 레벨(Non block-level scope)  
<pre>
<code>
if(true){
    var x = "x in block";
}
console.log(x);
//x in block
</code>
</pre>  
변수 x는 코드 블록 내에서 선언되었습니다.  
하지만 자바스크립트는 블록 레벨 스코프를 사용하지 않으므로 함수 밖에서 선언된 변수는 코드 블록 내에서 선언되었다할지라도 모두 전역 스코프을 갖게됩니다.  
따라서 변수 x는 전역 변수입니다.
  
  
# 함수 레벨 스코프(Function-level scope)  
<pre>
<code>
//전역 변수
var a = 10;

//즉시 실행 함수
(function(){
    //지역 변수 (함수 레벨 스코프)
    var b = 20;
})();

console.log(a);
//10
console.log(b);
//Uncaught ReferenceError: b is not defined
</code>
</pre>
자바스크립트는 함수 레벨 스코프를 사용한다. 즉, 함수 내에서 선언된 매개변수와 변수는 함수 외부에서는 유효하지 않습니다.  
따라서 변수 b는 지역 변수입니다.

<pre>
<code>
var x = 'global';

function foo(){
    var x = 'local';
    console.log(x);
}

foo();
//local
console.log(x);
//global
</code>
</pre>
전역변수 x와 지역변수 x가 중복 선언되었습니다.  
전역 영역에서는 전역변수만이 참조 가능하고 함수 내 지역 영역에서는 전역과 지역 변수 모두 참조 가능하나 위 예제와 같이 변수명이 중복된 경우, 지역변수를 우선하여 참조합니다.  

  

이어서 함수 내에 존재하는 함수인 **내부 함수**의 경우를 보겠습니다.
<pre>
<code>
var x = 'global';

function foo(){
    var x = 'local';
    console.log('=====foo=====');
    console.log(x);

    function bar(){
        console.log('=====bar=====');
        console.log(x);
    }
    bar();
}

foo();
console.log(x);
</code>
</pre>
>=====foo=====  
 local  
 =====bar=====  
 local  
 global  

**내부함수는 자신을 포함하고 있는 외부함수의 변수에 접근할 수 있습니다.**
이는 매우 유용합니다.  
클로저에서와 같이 내부함수가 더 오래 생존하는 경우, 타 언어와는 다른 움직임을 보입니다.

함수 bar에서 참조하는 변수 x는 함수 foo에서 선언된 지역변수입니다.  
이는 실행 컨텍스트의 스코프 체인에 의해 참조 순위에서 전역변수 x가 뒤로 밀렸기 때문입니다.
  
<pre>
<code>
var x = 100;

function foo(){
    x = 200;
    console.log('====foo====');
    console.log(x);
}

foo();
console.log('====global====');
console.log(x);
</code>
</pre>
>====foo====  
200  
====global====  
200  
  
함수(지역) 영역에서 전역변수를 참조할 수 있으므로 전역변수의 값도 변경할 수 있습니다.  
내부 함수의 경우, 전역변수는 물론 상위 함수에서 선언한 변수에 접근/변경이 가능합니다.  

<pre>
<code>
var x = 100;

function foo(){
    var x = 100;
    console.log('===foo===');
    console.log(x);

    function bar(){
        x = 200;
        console.log('===bar===');
        console.log(x);
    }
    bar();
}

foo();
console.log('===global===');
console.log(x);
</code>
</pre>
>===foo===  
100  
===bar===  
200  
===global===  
100  
중첩 스코프는 가장 인접한 지역을 우선하여 참조합니다.  
함수 bar에서 참조한 변수 x는 가강 인접한 지역인 함수 foo의 지역변수 x를 참조합니다.  
  

# 렉시컬 스코프
<pre>
<code>
var x = 1;

function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // ?
bar(); // ?
</code>
</pre>
위 예제의 실행결과를 예상해봅시다.
위 예제의 실행결과는 **함수 bar**의 상위 스코프가 무엇인지 따라 결정됩니다.  
두 가지 패턴으로 예측할 수 있는데
```
1. 함수를 어디서 호출하였는지에 따라 상위 스코프를 결정  
2. 함수를 어디서 선언하였는지에 따라 상위 스코프를 결정하는 것  
```
첫번째 방식으로 함수 bar의 상위 스코프를 결정한다면 함수 bar의 상위 스코프는  
**함수 foo**와 **전역**일 것이고,  
두번째 방식으로 함수 bar의 상위 스코프를 결정한다면 함수 bar의 상위 스코프는
**전역**일 것입니다.  
  
프로그래밍 언어는 이 두가지 방식 중 하나의 방식으로 함수의 상위 스코프를 결정합니다다.  
첫번째 방식을 **동적 스코프(Dynamic scope)** 라 하고,  
두번째 방식을 **렉시컬 스코프(Lexical scope)** 또는 **정적 스코프(Static scope)** 라 합니다.  
자바스크립트를 비롯한 대부분의 프로그래밍 언어는 **렉시컬 스코프**를 따른다.  
  
**렉시컬 스코프는 함수를 어디서 호출하는지가 아니라 어디에 선언하였는지에 따라 결정됩니다.**  
자바스크립트는 렉시컬 스코프를 따르므로 **함수를 선언한 시점에 상위 스코프가 결정됩니다.**  
함수를 어디에서 호출하였는지는 스코프 결정에 아무런 의미를 주지 않는다.  
  
위 예제의 함수 bar는 전역에 선언되었습니다. 따라서 함수 bar의 상위 스코프는 전역 스코프이고  
위 예제는 전역 변수 x의 값 1을 두번 출력합니다.  
  

# 암묵적 전역  
<pre>
<code>
// 전역 변수
var x = 10; 

function foo () {
  // 선언하지 않은 식별자
  y = 20;
  console.log(x + y);
}

foo();
// 30
</code>
</pre>
위의 예제에서 y는 선언하지 않은 식별자 입니다.  따라서 `y =20 `이 실행되면 참조 에러가 발생할 것처럼 보입니다.  
하지만 선언하지 않은 식별자 y는 마치 선언된 식별자처럼 동작합니다. 이는 선언하지 않은 식별자에게 값을 할당하면  
전역 객체의 프로퍼티가 되기 때문입니다.  
  
foo 함수가 호출되면 자바스크립트 엔진은 변수 y에 값을 할당하기 위해 먼저 스코프 체인을 통해 선언된 변수인지 확인합니다.  
이때 foo 함수의 스코프와 전역 스코프 어디에서도 변수 y의 선언을 찾을 수 없으므로 참조 에러가 발생해야 하지만 자바스크립트 엔진은  
`y = 20`을 `window.y = 20`으로 해석하여 프로퍼티를 동적 생성합니다. 결국 y는 전역 객체의 프로퍼티가 되어 마치 전역 변수처럼 동작합니다.  
이러한 현상을 `암묵적 전역(implicit global)`이라 한다.  
  
하지만 y는 변수 선언없이 단지 전역 객체의 프로퍼티로 추가되었을 뿐입니다. 따라서 y는 변수가 아닙니단.  
따라서 변수가 아닌 y는 `변수 호이스팅`이 발생하지 않는다.  
<pre>
<code>
// 전역 변수 x는 호이스팅이 발생한다.
console.log(x); // undefined
// 전역 변수가 아니라 단지 전역 프로퍼티인 y는 호이스팅이 발생하지 않는다.
console.log(y); // ReferenceError: y is not defined

var x = 10; // 전역 변수

function foo () {
  // 선언하지 않은 변수
  y = 20;
  console.log(x + y);
}
foo(); // 30
</code>
</pre>
또한 변수가 아니라 단지 프로퍼티인 y는 delete 연산자로 삭제할 수 있습니다.  
전역 변수는 프로퍼티이지만 delete 연산자로 삭제할 수 없습니다.  
<pre>
<code>
var x = 10; // 전역 변수

function foo () {
  // 선언하지 않은 변수
  y = 20;
  console.log(x + y);
}

foo(); // 30

console.log(window.x); // 10
console.log(window.y); // 20

delete x; // 전역 변수는 삭제되지 않는다.
delete y; // 프로퍼티는 삭제된다.

console.log(window.x); // 10
console.log(window.y); // undefined
</code>
</pre>
  
# 최소한의 전역변수 사용  
전역변수 사용을 최소화하는 방법 중 하나는 애플리케이션에서 전역변수 사용을 위해 다음과 같이 전역변수 객체 하나를 만들어 사용하는 것이다.  
<pre>
<code>
var MYAPP = {};

MYAPP.student = {
  name: 'Lee',
  gender: 'male'
};

console.log(MYAPP.student.name);
//Lee
</code>
</pre>  

# 즉시실행함수를 이용한 전역변수 사용 억제  
전역변수 사용을 억제하기 위해, 즉시 실행 함수(IIFE, Immediately-Invoked Function Expression)를 사용할 수 있다. 이 방법을 사용하면 전역변수를 만들지 않으므로 라이브러리 등에 자주 사용됩니다.  
즉시 실행 함수는 즉시 실행되고 그 후 전역에서 바로 사라집니다.  
<pre>
<code>
(function () {
  var MYAPP = {};

  MYAPP.student = {
    name: 'Lee',
    gender: 'male'
  };

  console.log(MYAPP.student.name);
}());

console.log(MYAPP.student.name);
</code>
</pre>
