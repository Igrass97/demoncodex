#finished 
**n !** **= n × ( n − 1 ) !**

``` js
const factorial = n => {
	if (n === 1) {
		return 1;
	}

	return n * factorial(n - 1);
}
```
