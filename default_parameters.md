## Default parameters



***기본값을 지정해주는 것***



```javascript
var template = (username = 'codestates') => {
    return `<div>
	${username}
</div>`
}

template(); // 인자가 없는 경우
/*
<div>
	codestates
</div>
*/

template('Ronaldo'); // 인자를 넣어주는 경우
/*
<div>
	Ronaldo
</div>
*/
```

