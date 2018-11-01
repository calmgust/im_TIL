## Rest parameters



```javascript
// ES5
function getMax(){ 
    var max = arguments[0];
    for(var i = 1; i < arguments.length; i++){
        if(max < arguments[i]){
            max = arguments[i];
        }
    }
    
    return max;
}

getMax([1, 3, 5, 6, 1]); // 6

//-----

//ES6
function getMax(...args){ // function getMax(a, b, ...args) => a와 b는 예외 지정 가능
    var max = args[0];
    for(var i = 1; i < arges.length; i++){
        if(max < args[i]){
            max = args[i];
        }
    }
    
    return max;
}
```



`arguments`는 array가 아니라 array like object

그렇기 때문에 forEach가 불가능



`...args`는 array이기 때문에 forEach가 가능



----



* **Rest parameters는 <u>비구조화 할당(destructuring assignment)</u>을 사용 시 더 강력한 기능을 구현 가능**

