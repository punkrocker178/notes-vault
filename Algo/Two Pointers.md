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
		nums[lastNonZeroIndex] = nums[j];
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

^424250

The `lastNonZeroIndex` is for readability and more straightforward to the problem. We can see this as `i` and `j`. 
The pattern here is using `j` for scanning the array and overwrite the positions `i(lastNonZeroIndex)` from the start if `nums[j]` is non zero. By doing this, we can move all non zero numbers to the start of the array. Leaving the remaining positions to be filled with 0.

[Example 2: Merge 2 sorted arrays](https://leetcode.com/problems/merge-sorted-array)
```typescript
// nums1: [1,2,3]
// nums2: [2,5,6]
// Output: [1,2,2,3,5,6]

// Avoid using nums1 directly because nums1 is overwritten by the 2 arrays.
let nums1Copy = nums1.slice(0, m);

for(let k = 0; k < m + n; k++) {
	if (j >= n || (i < m && nums1Copy[i] <= nums2[j])) {
	    nums1[k] = nums1Copy[i];
		i++;
	} else if (i >= m || (i < m && nums1Copy[i] > nums2[j])) {
        nums1[k] = nums2[j];
        j++;
    }
}
```
>**Note:** This leetcode problem requires modify `nums1` array inplace, so a copy of `nums1` is needed. If problem allow returning a new array, we can skip this step.

**Intuition**: use 2 indices `i` and `j` to track `nums1` and `nums2` respectively. If there is a smaller element between the 2 arrays, add it to the result array(`nums1`) and increment it's index.

**Edge case**:
To handle edge cases, we added the logic `j >= n`, `i >= m` to indicate that we have processed all elements of `nums1` or `nums2`, we just need to append remaining elements to the result array.
```typescript
// i track nums1
// j track nums2
nums1: [1]
nums2: []
// Output: [1]
// Because j >= n. Which is 0 >= 0

// Or case 2
nums1: []
nums2: [1]
// Output: [1]
// Because i >= m

```

[Example 3: Remove duplicates from sorted array]([Remove Duplicates from Sorted Array - LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/submissions/1633641235/))
```typescript
// Input: [0,0,1,1,1,2,2,3,3,4]
// Output: [0,1,2,3,4,_,_,_,_,_]
let i = 0;
let j = 1;
for (j = 1; j < nums.length; j++) {
	if (nums[j] != nums[i]) {
		nums[i + 1] = nums[j];
		i++;
    }
}
// nums at this point: [0,1,2,3,4,2,2,3,3,4]
//                                ^ Ignore the rest
return  i + 1;
```
The problem requires to modify array **in-place**. So we have to return number of unique numbers and ignore the remaining element beyond this point.
**Intuition**:
Based on the requirements, we can't use new array to append unique elements approach.
Instead, we will use `i` and `j` with different pace:
- Index `i` is used for indicating the current element to be scanned. 
- Index `j` is used for scanning array, if `nums[j] != nums[i]` then we will overwrite position `i+1` to become the new element to be scanned(`nums[j]`). 
- Loop ends when j  is at the last element, by this time our array will have all unique elements moved to the start of the array. Then we can return `i+1` to indicate the number of unique elements
This problem has the same pattern as [[#^424250|Example 1: Move Zeroes]] 

## Notes:
For opposite direction pointers:
- Imagine `i` and `j` can be seen as `left` and `right`

For different pace pointers:
- `i` is used as a slow pointer/current element to be process, if satisfy condition, increment it.
- `j` is used as a fast pointer, scanning the array to compare with `i`.