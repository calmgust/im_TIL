# checkpoint 1-3



### checkpoint 1: scope



1. 

```javascript
var x = 30;

function get(){
    return x;
}

var result = get(20); // 30

get() === get(20) === 30 // true
```



2. 

```javascript
var x = 30;

function get(x){
    return x;
}

var result = get(20); // 20

get(10); // 10
get(30); // 30
```



### 3.

```javascript
var x = 30; // global

function get(){
    return x;
}
function set(value){
    var x = value; // local
}

set(10);
var result = get(20); // 30
```



### 4.

```javascript
var x = 30;

function get(){
    return x;
}
function set(value){
    x = value; // global (전역에서 선언된 값을 변경)
}

set(10);
var result = get(20); // 10
```



5.

```javascript
var x = 30;

function get(x){
    return x; // 받아온 인자를 그대로 return
}
function set(value){
    x = value;
}

set(10);
var result = get(20); // 20
```



6.

```javascript
var x = 10;

function add(y){
    return x + y;
}

function strangeAdd(x){
    return add(x) + add(x);
}

var result = strangeAdd(5); // 30
```



7.

```javascript
var x = 10;

function outer(){
    var x = 20; //inner()의 return값
    function inner(){
        return x;
    }
    return inner();
}

var result = outer(); // 20
```



### 8.

```javascript
var x = 10; // global

function outer(){
    var x = 20;
    function inner(){
        x = x + 10;
        return x;
    }
    inner();
}

outer();

var result = x; // 10 (global을 참조)
```



9.

```javascript
var x = 10;

function outer(){
    x = 20; // global 값을 재설정
    function inner(){
        var x = x + 20; // local
        return x;
    }
    inner();
}

outer();

var result = x; // 20
```



10.

```javascript
var x = 10;

function outer(){
    x = 20; // global 값을 재설정
    function inner(){
        x = x + 20; // global에서 재설정 된 값을 투입
    }
    inner();
}

outer();

var result = x; // 40
```





----



### checkpoint 2: closure



1. 아래 코드에서, 어떤 function이 closure로 간주됩니까?

```javascript
var seenYet = function () {
    var archive = {};
    return function (val) {
        if (archive[val]) {
            return true;
        }
        archieve[val] = true;
        return false;
    }
}
```

**=> The anonymous function returned by the function named 'seenYet'**



2. total의 값은 무엇인가요?

```javascript
var add = function (x) {
    var sum = function (y) {
        return x + y;
    }
    return sum;
}

var foo = add(1);
foo(3); // 4
var total = foo(6); // 7
```



3. 다음 함수(multiplyByX, multiplyByFive)중 closure 사용을 보여주는 함수는 무엇입니까?

```javascript
var multiplyByX = function (x) {
  return function (y) {
    return x * y;
  }
}
var multiplyBy5 = multiplyByX(5);
multiplyBy5(4); // 20

var multiplyByFive = function() {
  return function (y) {
    return 5 * y;
  }
}

var multiplyBy5 = multiplyByFive();
multiplyBy5(4); // 20
```

**=> multiplyByX uses closure because the returned function still has access to the value x.**



---



### checkpoint 3: this



1. 'this' 키워드가 무엇을 나타냅니까?

**=> An object that the invoked function points to when executing.**



2. result의 값은 무엇?

```javascript
var x = 10;
var strangeAdd = function (y) {
  var x = 20;
  return this.x + y
};
result = strangeAdd(10); // 20
```



3. 'this' 키워드의 의미를 어떻게 결정할까요?

**=> Look to where the function is called at call time to determine how it is called and evaluate from there.**



4. 'this'가 가르키는 문맥을 식별하는데 적용되는 다섯가지 패턴은 무엇이 있는지 간단히 설명

   1-1. Global: window

   1-2. Function invocation: window

   1-3. Method invocation: 부모 object

   1-4. Construction mode(new 연산자로 생성된 function 영역의 this): 새로 생성된 객체

   1-5. .call or .apply invocation: call, apply의 첫 번째 인자로 명시 된 객체

5. console의 무엇이 찍힐까요?

```javascript
function foo () {
    console.log(this);
}

foo(); // window
```



6. console의 무엇이 찍힐까요?

```javascript
var obj = {
    foo: function () {
        console.log(this);
    }
}

obj.foo(); // obj (부모 object)
```



7. console의 무엇이 찍힐까요?

```javascript
var obj = {
    foo: function () {
        console.log(this);
    }
}

var fn = obj.foo;
fn(); // window
```



8. console.의 무엇이 찍힐까요?

```javascript
var obj = {
  foo: function(){
    console.log(this);
  }
}
var obj2 = {
  foo: obj.foo
}

obj.foo.call(obj2); // obj2
```

