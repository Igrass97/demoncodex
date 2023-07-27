#finished
Merge sort is a recursive algorithm that continuously splits the array in half until it cannot be further divided i.e., the array has only one element left (an array with one element is always sorted). Then the sorted subarrays are merged into one sorted array.

## Procedure
merge: function that merges two sorted arrays
1. Compare the first index of each sorted array. Remove the smaller one from the corresponding array and push it to a results array.
2. If there are still elements on either array, repeat. When there is an empty array, continue.
3. One of the arrays will always hold values, and these values will be greater than the results, so it's safe to return the concatenation results + Array1 + Array2
merge sort:
1. If the length of the array is 1 return it (the array is sorted)
2. Divide the array in two halves and return merge(mergeSort(half1), mergeSort(half2))

## Analysis
**Time Complexity**: T(n) = 2T(n/2) + θ(n)
**Time Complexity:** O(N), In merge sort all elements are copied into an auxiliary array. So N auxiliary space is required for merge sort.


``` js
const mergeSort = nums => {
	const merge = (a, b) => {
		const results = [];

		while (a.length && b.length) {
			if (a[0] < b[0]) {
				results.push(a.shift());
			} else {
				results.push(b.shift());
			}
		}

		return [...results, ...a, ...b];
	}

	if (nums.length === 1) return nums;

	return merge(
		mergeSort(nums.slice(0, Math.floor(nums.length / 2))),
		mergeSort(nums.slice(Math.floor(nums.length / 2)))
	);
}
```