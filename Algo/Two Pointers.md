**_Time complexity: O(n)_**
**_Space complexity: O(1)_**

A common technique to process arrays, strings and linked list. This technique is a goto method to reduce the time complexity of Bruteforce approach.

Can be used in many operations:
- Search (Find sum, Remove duplicates)
- Reverse (linked list, arrays)
- Merge sorted arrays
- Partrition arrays
- Subarray/Substring problems
- Triplet problem (3Sum)

## Patterns
### 1. Two pointer at both ends, moving opposite direction
We will have 2 pointer `i` and `j` at the opposite end of the array. Depend on the problem, we can move both pointers or one at a time.
Example 1:
```typescript
// Reverse array
// [1,2,3,4,5]

let i = 0;
let j = nums.length - 1;
while(i < j) {
	swap(nums[i], nums[j]);
	i++;
	j--;
}
// [5,4,3,2,1]
```
The above example move two pointers at a time to swap elements from start to end. We will stop when `i == j`

Example 2:
```typescript
// Two sum. Find a pair in array that match target x
// In this example, array needs to be sorted first
let i = 0;
let j = nums.length - 1;
while(i < j) {
	let sum = nums[i] + nums[j];
	if (sum > x) {
		j--;
	} else if (sum < x) {
		i++;
	} else {
		break;
	}
}

// target x doesn't exist in array
if (i == j) {
	return null;
}

return [i, j];

```
The above example is a different problem but same pattern can be applied. Since the array is sorted, we now know that `sum > x` means our indices combination are too big, we need to decrement `j` to give a smaller sum. If `sum < x` means we need to increment `i` to find a larger sum;
### 2. Two pointer move at same direction, different paces
1. Slow & fast pointer 
	See [[Linked list#Common techniques]]
2. Different pace
	[Example 1: Move zeroes](https://leetcode.com/problems/move-zeroes/)
```typescript
// Move zeroes to end of array
// Input: [0,1,0,3,5,12]
// Output: [1,3,5,12,0,0]

let lastNonZeroIndex = 0;
for(let j = 0; j < nums.length; i++) {
	if (nums[j] != 0) {
		// Overwrite original value
		swap(nums[lastNonZeroIndex], nums[j]);
		lastNonZeroIndex++;
	}
}
// Nums array after overwrite: [1,3,5,12,5,12]
// Set zeroes beyond lastNonZeroIndex
for (let i = lastNonZeroIndex; i < nums.length; i++) {
	nums[i] = 0;
}
// Nums array: [1,3,5,12,0,0]
```
The `lastNonZeroIndex` is for readability and more straightforward to the problem. We can see this as `i` and `j`. The pattern here is using `j` for scanning the array and overwrite the positions `i(lastNonZeroIndex)` from the start if `nums[j]` is non zero. By doing this, we can move all non zero numbers to the start of the array. Leaving the remaining positions to be filled with 0.

[Example 2: Merge 2 sorted arrays](https://leetcode.com/problems/merge-sorted-array)
```typescript
// nums1: [1,2,3]
// nums2: [2,5,6]
// Output: [1,2,2,3,5,6]


```
