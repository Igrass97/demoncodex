#finished 
Is a non-comparison sort. 
It works by creating 10 buckets (one for each digit in the decimal system).

Loops through the array N times, where N is the longest number length. Each element is placed in the corresponding bucket (and removed from the original array) based on the digit on the decimal place of interest.

When every element from the array is assigned to a bucket, de-queue each bucket into the main array. (de-queue: removing elements from the start of the array).

## Procedure
1. Get the maximum number length from the array, call it N.
2. Create an array of 10 arrays for the buckets.
3. Until the array is empty, take the first element of the array and put into the corresponding bucket, based on the digit in the decimal place of interest. (given by the loop control variable).
4. Once the array is empty, de-queue each bucket into the main array. Repeat N times, one for each decimal place of the numbers.

## Analysis
**Time Complexity**: It has a time complexity of **O(d * (n + b))**, where d is the number of digits, n is the number of elements, and b is the base of the number system being used.
**Space Complexity**: Radix sort also has a space complexity of **O(n + b),** where n is the number of elements and b is the base of the number system.

![[Pasted image 20230716134653.png]]