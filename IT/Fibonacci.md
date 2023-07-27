#finished
The first number of the pattern is 0, the second number is 1, and each number after that is equal to adding the two numbers right before it together.

``` js
const fibonacci = (n) => {
	if (n === 1 || n === 0) {
		return n;
	}

	return fibonacci(n - 1) + fibonacci(n - 2);
}
```
