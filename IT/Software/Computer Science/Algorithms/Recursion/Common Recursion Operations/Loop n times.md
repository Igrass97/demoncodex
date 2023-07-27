#finished

``` js
const recursiveFor = (callback, times) => {
	if (times === 1) {
		return callback(times);
	}

	callback(times);

	recursiveFor(callback, times - 1);
}
```