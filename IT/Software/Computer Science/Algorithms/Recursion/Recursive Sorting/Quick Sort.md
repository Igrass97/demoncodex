#finished
Quicksort is a divide-and-conquer algorithm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot.

Then returns Array1 + Pivot + Array2 concatenated.

The subarrays are sorted recursively with quick sort, and when you get arrays of length 1 or 0, quick sort will return.

## Procedure

1. If array length is 0 or 1, return the array. If not, continue
2. Grab a pivot (usually the last element of the array)
3. Split the array into two arrays. Array1 will hold values smaller than the pivot, and Array2 will hold values higher than the pivot.
4. Return a concatenation of: quick sorted Array1 + Pivot + quick sorted Array2

## Analysis
**Worst Case:*** O(N2)
**Auxiliary Space:*** O(1)

``` js
const quickSort = nums => {
	if (nums.length <= 1) return nums;

	const pivot = nums.pop();

	const left = [];
	const right = [];

	nums.forEach(n => {
		if (n > pivot) {
			right.push(n);
		} else {
			left.push(n);
		}
	});

	return [...quickSort(left), pivot, ...quickSort(right)];
}
```
