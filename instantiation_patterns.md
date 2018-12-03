# Instantiation Patterns



instantiate => 예시하다 / 구체적 예를 들어 나타내다



## 0. JavaScript의 Class



JavaScript에 Class가 나오기 전에 사용하던 4가지 Class 선언 방식

Class는 **하나의 정형화된 모델**을 만들어 두고, 그 **모델을 기반으로 한 인스턴스(복제품)를 만들기 위해** 사용

마치 공장에서 같은 규격의 제품들을 찍어내는 것과 비슷



ex)

Car라는 객체는 항상 position이라는 property와 move라는 method를 갖는다고 가정

그리고 Car1, Car2, Car3, … 매우 많은 Car들을 사용하는 프로그램을 작성한다고 했을 때, 많은 Car들을 하나하나 변수로 선언해주는 것은 많은 시간이 필요

Car라는 모델을 만들어 두고, 비슷한 객체들을 찍어내는 기능

`찍어 내는 기능`은 함수를 이용해서 표현할 수 있다는 점





## 1. Functional

Functional Instantiation 방식으로 자동차 공장을 만들어 보기

말 그대로 **함수를 이용해서 찍어내는 방식**



```javascript
var Car = function(){ // 1. 먼저 Car라는 함수를 만들어 주기

	var someInstance = {}; // 2. 함수를 실행했을 때, 찍어내 줄 객체를 선언 / 물론, return을 해줘야 함수의 결과로 객체가 나옴   
    
    someInstance.position = 0; // 3. someInstance의 position을 0으로 초기화해준다 / Car 함수가 실행되어 나온 인스턴스의 position 초기값은 항상 0일 것
   
    someInstance.move = function(){ // 4(1). 이제 이렇게 Car들을 찍어낼 수 있다
        this.position += 1;
    }
    
    return someInstance;
};

var car1 = Car();
var car2 = Car();
car1.move(); // 4(2). car1.move()를 실행한 후의 car1을 console.log로 찍어보면 position이 1인 것을 확인 가능
```



```javascript
var Car = function(position){ // 이렇게 초기 위치를 지정해 줄 수도 있다
    
    var someInstance = {};
    
    someInstance.position = position; // <= 인자
    someInstance.move = function(){
        this.position += 1;
    }
    
    return someInstance;
}

var car1 = Car(1); // 인자 값을 1로 지정
var car2 = Car(5); // 인자 값을 5로 지정
```





## 2. Functional Shared



```javascript
var extend = function(to, from){ // 3. someInstance와 someMethods를 합치는 extend 함수를 만들어서 Car 함수 내부에서 합쳐줌
    for(var key in from){
        to[key] = from[key]
    }
}

var someMethods = {}; // 2(1). 메소드를 담아줄 객체를 생성 (모든 메소드는 someMethods에 담을 것)
someMethods.move = function(){ // 2(2). 메소드를 담아줌
    this.position += 1;
};

var Car = function(position){ // 1. 먼저 Car 함수를 선언해 줍니다. 바로 position을 someInstance의 property로 넣어준 것 외에는 다른 부분이 없습니다.
    
    var someInstance = {
        position: position
    };
    extend(someInstance, someMethods);
    return someInstance;
};


var car1 = Car(5);
var car2 = Car(10); // 이제 공장처럼 차를 찍어낼 수 있게 되었습니다.

```

***Functional Shared  방식을 사용하는 이유***

* Functional  방식은 인스턴스를 생성할 때마다 모든 메소드를 someInstance에게 할당하므로, 각각의 인스턴스들이 메소드의 수 만큼의 메모리를 더 차지함

* Functional Shared 방식을 사용하면, someMethods라는 객체에 있는 메소드들의 메모리 주소만을 참조하기 때문에 **<u>메모리 효율이 좋아집니다.</u>** 


<img width="499" alt="2018-10-31 21 42 14" src="https://user-images.githubusercontent.com/40155174/47788753-f78d6e80-dd55-11e8-8759-7f03fbbc7490.png">





## 3. Prototypal



먼저 Functional Shared 방식과 비슷하게 코드를 작성

```javascript
var someMethods = {};

someMethods.move = function(){
    this.position += 1; 
};

var Car = function(position){
    var someInstance = {}; // <= 이 부분만 변경!!
    someInstance.position = position;
    return someInstance;
};
```



```javascript
var someMethods = {};

someMethods.move = function(){
    this.position += 1; 
};

var Car = function(position){
    var someInstance = Object.create(someMethods); // <= 이 부분만 변경!!
    someInstance.position = position;
    return someInstance;
};

var car1 = Car(5);
var car2 = Car(10);
```



**`Object.create`는 특정 객체를 프로토타입으로 하는 객체를 생성해 주는 함수**





## 4. Pseudoclassical



```javascript
var Car = function(position){ // 1. 먼저 이렇게 코드를 작성
    this.position = position;
};

Car.prototype.move = function(){ // 2. 메소드를 프로토 타입으로 만들어 준다
    this.position += 1;
};

var car1 = new Car(5);
var car2 = new Car(10); // 3. 하지만 이렇게 찍어낼 때에 new operator를 붙여야
```



**`new`operator를 붙여줘야한다**





---



#### slack study

```javascript
// Five Patterns of Instance Creation

// 1. Functional pattern
function Person(name) {
	this.name = name;
	this.getName = function() {
		return this.name;
	}
	return instanceOfPerson;
}
var p = Person.call(Object.create({}), "anonymous");


// 2. Functional-shared pattern
var extend = function(obj) {
	for(var i=1; i<arguments.length; i++) {
		for(var key in arguments[i]) {
			obj[key] = arguments[i][key];
		}
	}
}
function Person(name) {
	this.name = name;
	extend(this, instanceMethodsOfPerson);
}
var instanceMethodsOfPerson = {};
instanceMethodsOfPerson.getName = function() {
	return this.name;
}
var p = Person.call(Object.create(instanceMethodsOfPerson), "anonymous")


// 3. prototypel pattern
function Person(name) {
	this.name = name;
	
	return this;
}
Person.prototype.getName = function() {
	return this.name;
}

var p = Person.call(Object.create(Person.prototype), "anonymous");


// 4. pseudoclassical pattern
function Person(name) {
	this.name = name;
}
Person.prototype.getName = function() {
	return this.name;
}

var p = new Person("anonymous");


// 5. class pattern [ ECMAScript6 ]
class Person {
	constructor(name) {
		this.name = name;
	}

	getName() {
		return this.name;
	}
}

const p = new Person("anonymous");
```



