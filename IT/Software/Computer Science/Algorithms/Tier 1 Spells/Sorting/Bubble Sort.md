#finished
**Bubble Sort** is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order. This algorithm is not suitable for large data sets as its average and worst-case time complexity is quite high.

## Procedure
1. Loop through the array swapping adjacent elements if they are not ordered.
2. If no swaps done, array is sorted. If a swap was performed in the iteration, repeat

## Analysis
**Time Complexity:** O(N2)  
**Auxiliary Space:** O(1)

``` js
const bubbleSort = nums => {
	let swapped = false;

	for (let i = 0; i < nums.length; i++) {
		if (nums[i] > nums[i + 1]) {
			swapped = true;

			const aux = nums[i];
			nums[i] = nums[i + 1];
			nums[i + 1] = aux;
		}
	}

	return nums;
}
```
