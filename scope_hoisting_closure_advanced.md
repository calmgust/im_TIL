# scope



#### what is a scope?

변수는 어떠한 환경 내에서만 사용가능하며, 프로그래밍 언어는 각각의 변수 접근 규칙을 갖고 있다.

* 변수와 그 값이 어디서부터 어디까지가 유효한지를 판단하는 범위
* scope는 변수 접근 규칙에 따른 **유효범위**를 의미
* JavaScript에서는 함수가 선언되는(Lexical) 동시에 자신만의 scope를 가짐



```javascript
var greeting = 'Hello';

function greetSomeone(){
    var firstName = 'Josh';
    return greeting + ' ' + firstName;
}

greetSomeone(); // => Hello Josh
firstName; // => ReferenceError
```





##### Lexical(Static) Scope Vs. Dynamic Scope

* Lexical(static) Scope: 유효범위가 코드를 작성될 때 결정됨
* Dynamic Scope: 유효범위가 실행 순서에 의해 결정됨





#### Rule 1: Local Scope Vs. Global Scope

* Scope는 중첩이 가능
* 하위 Scope가 상위 Scope의 변수 접근 가능

```javascript
var hero = aHero();
var newSaga = function(){
    var foil = aFoil();
    var saga = function(){
        var deed = aDeed();
        console.log(hero+deed+foil);
    };
    saga();
    saga();
};
newSaga();
newSaga();
```

* Global Scope는 어디에서도 접근 가능
* 지역변수는 함수 내에서 전역변수보다 높은 우선순위





#### Rule 2: Block Level Vs. Function Level

JavaScript는 기본적으로, function level의 scoping 규칙을 따름



var 와 let의 차이점 (function level / block level)

```javascript
for(var i = 0; i < 5; i++){
    console.log(i); // 다섯 번 iteration
}
console.log('final i : ', i); // final i : 5
```



```javascript
for(let i = 0; i < 5; i+=1){
    console.log(i); // 다섯 번 iteration
}
console.log('final i : ', i); // ReferenceError
```



* ***let과 const keyword는 block을 벗어나면, 접근 불가능***
* ***let과 const는 var로 정의된 변수를 재정의할 수 없음***
* ***const는 불변(immutable)한 값으로, 다시 값을 할당할 수 없음***





#### Rule 3: 전역 변수와 window객체

* 함수의 외부에서 선언된 모든 변수는 전역 범위
* 전역 범위를 대표하는 객체 : window
* 모든 전역 변수는 window 객체와 연결

```javascript
var name = "Paul";
console.log(window.name); // Paul
```





#### Rule 4: 선언 없이 초기화된 변수는 전역 변수

```javascript
function showAge(){
    // age는 전역 변수.
    age = 90;
    console.log(age);
}

showAge(); // 90
console.log(age); // 90
```





#### Rule 5: Hoisting

* 변수 선언은 범위에 따라 **선언**과 **할당**으로 분리됨
* JavaScript 엔진이 내부적으로 **변수 선언을 Scope의 상단으로 끌어 올림(hoist)**



---



## scope (advanced)



#### review

* scope는 중첩 가능
* 기본적으로 function level scope
* 전역 변수는 window 객체와 연결(node.js에서는 **global**)
* var 변수 선언은 scope 상단으로 hoisting됨





##### Lexical(Static) Scope Vs. Dynamic Scope

* 유효범위(scope): 코드를 **작성할 때(lexical)** 결정됨
* this(execution context): 함수가 **실행될 때(run-time, dynamically)** 결정됨





##### let, const, var

* let / const: **block scope**를 따르는 변수 선언

* var: function scope를 따르는 변수 선언

* **let, const는** var처럼 **hoist되지 않음**

  ```javascript
  console.log(a); // undefined
  var a = 'hello';
  
  console.log(b); // ReferenceError
  let b = 'world';
  ```

* 같은 scope 내에서 let, const를 이용하여 다시 정의할 수 없음

* const는 상수 선언

  ```javascript
  let b = 'first';
  let b = 'second'; // SyntaxError
  
  const c = 'this is constant';
  c = 'try to change'; // TypeError
  ```



  ```javascript
  (function() {
      var a = 'immediately invoked';
      console.log(a);
  })();
  
//-----
// let을 이용하여 IIFE를 대신할 수 있다

  {
      let a = 'immediately invoked';
      console.log(a);
  }
  ```





---



# closure (advanced)



#### review

* *외부함수의 변수에 접근할 수 있는 내부 함수*
* **함수를 return하는 형태로 보통 사용**





#### currying

```javascript
function sum3(x, y, z) {
    return x + y + z;
}

console.log(sum3(1, 2, 3)) // 6
```



```javascript
function sum3(x) {
    return function(y) {
        return function(z) {
            return x + y + z;
        };
    };
}

console.log(sum3(1)(2)(3)) // 6
```





#### arrow function

```javascript
function sum3(x) {
    return y => {
        return z => {
            return x + y + z;
        }
    }
}

console.log(sum3(1)(2)(3)) // 6
```



```javascript
var sum3 = x => y => z => x + y + z;

console.log(sum3(1)(2)(3)) // 6
```

