# Promise (JavaScript)



## 1. Promise

***"A promise is an object that may produce a single value some time in the future"***



**프로미스**는 <u>자바스크립트 비동기 처리에 사용되는 객체</u>

**자자스크립트의 비동기 처리**란 <u>특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성</u>





## 2. Promise가 필요한 이유

프로미스는 ***주로 서버에서 받아온 데이터를 화면에 표시할 때 사용***

일반적으로 웹 애플리케이션을 구현할 때 서버에서 데이터를 요청하고 받아오기 위해 아래와 같은 API를 사용

```javascript
$.get('url 주소/products/1', function (response) {
    // ...
});
```

위 API가 실행되면 서버에다가 '데이터 하나 보내주세요'라는 요청을 보내는데, 여기서 *<u>데이터를 받아오기도 전에 마치 데이터를 다 받아온 것 마냥 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜹니다</u>*. 이와 같은 문제점을 해결하기 위한 방법 중 하나가 프로미스입니다.





## 3. Promise 코드 - 기초

프로미스가 어떻게 동작하는지 이해하기 위한 간단한 예제 ajax 통신 코드

```javascript
function getData (callbackFunc) {
    $.get('url 주소/products/1', function (response) {
        callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
    });
}

getData(function (tableData) {
    console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});
```

위 코드는 jQoery의 ajax 통신을 이용하여 지정한 url에서 1번 상품 데이터를 받아오는 코드

비동기 처리를 위해 프로미스 대신에 콜백 함수를 이용

위 코드에 프로미스를 적용하면 아래와 같은 코드가 됩니다.

```javascript
function getData (callback) {
    //new Promise() 추가
    return new Promise(function (resolve, reject) {
        $.get('url 주소/product/1', function (response) {
            // 데이터를 받으면 resolve() 호출
            resolve(response);
        });
    });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function (tableData) {
    // resolve()의 결과 값이 여기로 전달 됨
    console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});
```

콜백 함수로 처리하던 구조에서 `new Promise()`, `resolve()`, `then()` 와 같은 프로미스 API를 사용한 구조로 바뀜





## 4. Promise의 3가지 상태(states)

프로미스를 사용할 때 알아야 하는 가장 기본적인 개념이 바로 프로미스의 상태(state)

여기서 말하는 상태란 프로미스의 처리 과정

##### 상태 === 프로미스의 처리 과정



`new Promise()`로 프로미스를 생성하고 종료될 때까지 3가지 상태

* ***Pending(대기)*** : **비동기 처리 로직이 아직 완료되지 않은 상태**
* ***Fulfilled(이행)*** : **비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태**
* ***Rejected(실패)*** : **비동기 처리가 실패하거나 오류가 발생한 상태**



#### Pending (대기)

```javascript
new Promise();
```

**`new Promise()` 메서드를 호출**하면 **Pending(대기) 상태**가 됩니다.

```javascript
new Promise(function (resolve, reject) {
    // ...
});
```

이렇게 `new promise()` 메서드를 호출할 때 콜백 함수의 인자로 resolve, reject에 접근 가능



#### Fulfilled (이행)

```javascript
new Promise(function (resolve, reject) {
    resolve();
});
```

콜백 함수의 인자 resolve를 아래와 같이 실행하면 Fufilled(이행) 상태가 된다.

```javascript
function getData() {
    return new Promise (function (resolve, reject) {
        var data = 100;
        resolve(data);
    });
}

// resolve()의 결과 값 data를 resolveData로 받음

getData().then(function (resolveData) {
    console.log(resolveData); // 100
});
```

이행 상태가 되면 아래와 같이 `then()`을 이용하여 처리 결과 값을 받을 수 있음

**`프로미스의 '이행'상태를 좀 다르게 표현해보면 '완료'입니다.`**



#### Rejected (실패)

```javascript
new Promise(function (resolve, reject) {
    reject();
});
```

`new Promise()`로 프로미스 객체를 생성하면 콜백함수 인자로 resolve와 reject를 사용할 수 있음

여기서 reject인자로 reject() 메서드를 실행하면 Rejected(실패) 상태가 됩니다.

```javascript
function getData() {
    return new Promise(function (resolve, reject) {
        reject(new Error("Request is failed"));
    });
}

// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function (err) {
    console.log(err); // Error: Request is failed
});

//-----
// 사용법
.then(resolve, reject)
.then(resolve).catch(reject)
```

![2018-11-21 19 53 19](https://user-images.githubusercontent.com/40155174/48836836-292eae00-edc7-11e8-9a17-628559e04c82.png)





## 5. Promise 코드 - 쉬운 예제

```javascript
function getData() {
    return new Promise(function (resolve, reject) {
        $.get('url 주소/products/1', function (response) {
            if (response) {
                resolve(response);
            }
            reject(new Error("Request is failed"));
        });
    });
}

// Fullfiled 또는 Rejected의 결과 값 출력
getData().then(function (data) {
    console.log(data); // response 값 출력
}).catch(function (err) {
    console.error(err); // Error 출력
})
```

위 코드는 서버에서 제대로 응답을 받아오면 resolve() 메서드를 호출하고, 응답이 없으면 reject() 메서드를 호출하는 예제

호출된 메서드에 따라 then()이나 catch()로 분기하여 데이터 또는 오류를 출력





## 6. 여러 개의 Promise 연결하기 (Promise Chaining)

프로미스의 또 다른 특징은 여러 개의 프로미스를 연결하여 사용할 수 있다는 점

앞 예제에서 then() 메서드를 호출하고 나면 새로운 프로미스 객체가 반환

```javascript
function getData() {
    return new Promise({
        // ...
    })
}

// then() 으로 여러 개의 프로미스를 연결한 형식
getData()
    .then(function (data) {
    // ...
})
    .then(function () {
    // ...
})
    .then(function () {
    // ...
});
```

비동기 처리 예제에서 가장 흔하게 사용되는 `setTimeout() API` 를 사용

```javascript
new Promise(function(resolve, reject) {
    setTimeout(function () {
        resolve(1);
    }, 2000);
})
    .then(function (result) {
    console.log(result); // 1
    return result + 10;
})
    .then(function (result) {
    console.log(result); // 11
    return result + 20;
})
    .then (function (result) {
    console.log(result); // 31
});
```

위 코드는 프로미스 객체를 하나 생성하고 `setTimeout()`을 이용해 2초 후에 `resolve()`를 호출하는 예제

`resolve()`가 호출되면 프로미스가 대기 상태에서 이행 상태로 넘거가기 때문에 첫 번째 `.then()`의 로직으로 넘어갑니다. 두 번째 `.then()`에서도 마찬가지로 바로 이전 프로미스의 결과 값 11을 받아서 20을 더하고 다음 `.then()` 으로 넘겨줍니다. 마지막 `.then()`에서 최종 결과 값 31을 출력합니다.





