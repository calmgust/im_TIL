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



