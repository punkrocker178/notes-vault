[What is Sliding Window Algorithm? Examples? - Stack Overflow](https://stackoverflow.com/questions/8269916/what-is-sliding-window-algorithm-examples)

This technique is commonly used in algorithms like finding:
- Subarrays with a specific sum or largest sum
- The longest substring with unique characters
- Other problems requires fixed size window to process element efficiently

### Brute force approach:
**Time complexity: O(n * k)**

Outer loop is looping through n items
Inner loop is looping through k items
Increment window by 1 step after inner loop is done
![O(n * k) visualisation](https://i.sstatic.net/2Dneo.png)

## Optimized approach
**Time complexity: O(n)

Instead of looping through k items of each Outer loop iteration.
We can calculate the initial window value, then use that value to calculate the next window.

1. Initialize the window
2. Increment the window position by 1
3. By doing that, we are removing the previous window element (i - 1) and add a new last window element (i + k -1).
4. After calculation, window size remain the same and window position is incremented by 1.

![O(n) visualization](https://i.sstatic.net/zsGl7.png)