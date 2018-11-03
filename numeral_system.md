# Numeral system



* 10진수 => 16진수

```javascript
var dec = 123; 
var hex = dec.toString(16); // === "7b"
```



* **10진수 => 2진수**

```javascript
var dec = 123; 
var bin = dec.toString(2); // === "1111011"
```



* 16진수 => 10진수

```javascript
var hex = "7b"; 
var dec = parseInt(hex, 16); // === "123"
```



* 16진수 => 2진수 (10진수로 바꿨다가 다시 2진수로 바꾼다)

```javascript
var hex = "7b"; 
var bin = parseInt(hex, 16).toString(2); // === "1111011"
```



* 2진수 => 10진수

```javascript
var bin = "1111011"; 
var dec = parseInt(bin, 2); // === "123"
```



* 2진수 => 16진수 (10진수로 바꿨다가 다시 2진수로 바꾼다)

```javascript
var bin = "1111011"; 
var hex = parseInt(bin, 2).toString(16); // === "7b"
```



*** 8진수는 위의 2나 16등이 있는 부분을 8로 바꾸면 서로 변환이 가능하므로 응용하면 된다.**

