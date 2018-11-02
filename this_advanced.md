# this (advanced)



### Binding Problem 

```javascript
function getSalaryFromServer(callback){
    setTimeout(function(){
        callback(10000);
    }, 1000);
}

function member(){
    return {
        first: 'Ingi',
        last: 'Kim',
        age: 40,
        printDetail: function(){
            getSalaryFromServer(function(salary){
                
                console.log(`Name: ${this.first} ${this.last}`);
                console.log(`Salary: ${salary}`);
            });
        }
    }
}

var ingi = member();
ingi.printDetail();

/*
Name: undefined undefined // => this가 window이기 때문에
Salary: 10000
*/
```



### Solution 1: USE `bind`

```javascript
function getSalaryFromServer(callback){
    setTimeout(function(){
        callback(10000);
    }, 1000);
}

function member(){
    return {
        first: 'Ingi',
        last: 'Kim',
        age: 40,
        printDetail: function(){
            getSalaryFromServer(function(salary){
                
                console.log(`Name: ${this.first} ${this.last}`);
                console.log(`Salary: ${salary}`);
            }, bind(this));
        }
    }
}
```



### Solution 2: USE Arrow function

```javascript
function getSalaryFromServer(callback){
    setTimeout(function(){
        callback(10000);
    }, 1000);
}

function member(){
    return {
        first: 'Ingi',
        last: 'Kim',
        age: 40,
        printDetail: function(){
            getSalaryFromServer(salary => {
                
                console.log(`Name: ${this.first} ${this.last}`);
                console.log(`Salary: ${salary}`);
            });
        }
    }
}
```



#### ARROW FUNCTION

* lexical `this`
  * ES5의 `this`는 **어디에서**보다 **어떻게** 호출되는지가 더 중요
  * arrow function을 사용한 함수는 **어디에서** 호출되는지만 고려해도 됨
* arguments를 바인딩하지 않음
* call, apply의 this 바인딩은 무시됨



### REST PARAMETERS

arguments를 받는 새로운 방법

```javascript
function foo(n){
    var f = (...args) => args[0] + n;
    return f(2);
}

foo(1); // 3
```



```javascript
function multiply(multiplier, ...theArgs){
    return theArgs.map(function(element){
        return multiplier * element;
    });
}

var arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```



#### 어느 곳에 Arrow function을 쓰는 것이 좋을까?

```javascript
var obj = {
    i: 10,
    b: () => console.log(this.i, this), // ?
    c: function(){
        console.log(this.i, this) // ?
    }
}
```



```javascript
var Foo = () => {};
var foo = new Foo(); // ?
```

