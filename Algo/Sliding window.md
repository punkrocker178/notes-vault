[What is Sliding Window Algorithm? Examples? - Stack Overflow](https://stackoverflow.com/questions/8269916/what-is-sliding-window-algorithm-examples)

This technique is commonly used in algorithms like finding:
- Subarrays with a specific sum or largest sum
- The longest substring with unique characters
- Other problems requires fixed size window to process element efficiently

## Problems with fixed window size
### Brute force approach:
**Time complexity: O(n * k)**

Outer loop is looping through n items
Inner loop is looping through k items
Increment window by 1 step after inner loop is done
![O(n * k) visualisation](https://i.sstatic.net/2Dneo.png)

### Optimized approach
**Time complexity: O(n)

Instead of looping through k items of each Outer loop iteration.
We can calculate the initial window value, then use that value to calculate the next window.

1. Initialize the window
2. Increment the window position by 1
3. By doing that, we are removing the previous window element (i - 1) and add a new last window element (i + k -1).
4. After calculation, window size remain the same and window position is incremented by 1.

![O(n) visualization](https://i.sstatic.net/zsGl7.png)

## Problem with dynamic size
Problems: 
1. https://leetcode.com/problems/minimum-size-subarray-sum

### O(n^2) Approach
We will start with window size = 1, then increment the window size until sum >= target.
We will use the optimized approach by calculating the initial sum. Then we will move the window by 1 position at a time, and calulate the sum by removing the last element and append the next element to the window: `sum -= sum[i -1]; sum += sum[i + k -1]`

### O(n) Approach
Instead of brute forcing the optimal `windowSize`. We can accumulate the sum values to find the smallest count of elements that >= `target`.  
Lets think of this way, we will accumulate the values until we meet the `target`. We then want to count all the values that have been accumulated. In order to minimize the count, we will try to reduce the first element of the accumulated array. If accumulated sum < `target`, we will continue to append a next value to the accumulated array. Then we rinse and repeat until we find the smallest count.

In short, we will move & resize the window until it has the smallest size that has `sum` >= `target`
1. Traverse the `nums` array and sum elements until sum is >= `target`.
2. Count elements that have made the sum. If count is lesser than the previous count, update count.
3. Then increment `left` index (the start of window) by 1 to reduce the sum.
4. If sum is < `target`. Then we repeat 1
5. Return count after loop ends. If count doesn't update, return 0