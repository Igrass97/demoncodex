#finished 
Loops over the array and finds the exact place to insert each number into the left part of the array which is always sorted.
Compares each number with the left part of the array, swapping elements to the right until it inserts it on the right place

## Procedure
1. Starting from index n=1, grab the current number.
2. Starting from index j=n-1, loop backwards moving to the right all numbers that are greater than the current number.
3. When a value smaller than the current number is found, insert current number in the next position.

## Analysis
**Time Complexity:** O(N^2)   
**Auxiliary Space:** O(1)

``` js
const insertionSort = nums => {
	for (let i = 1; i < nums.length; i++) {
		const numberToInsert = nums[i];
		
		for (let j = i - 1; j >= 0 && nums[j] > numberToInsert; --j) {
			nums[j + 1] = nums[j];
		}

		nums[j + 1] = numberToInsert;
	}

	return nums;
}
```
