_Reference: Qwen3-32B model_
## Definition
Is a brute force method but smarter. The algorithm will explore all the possibilities recursively and build the solution step by step. When a certain path doesn't work or already complete, it will undo (backtrack) and try another solution.

## Core Concept
Think of backtracking as **exploring a maze** :
- You try a path forward
- If you hit a dead end, you go back and try a different path
- Continue until you find the exit or exhaust all possibilities

## Common applications
1. Permutation generation
2. Sudoku solver
3. Subset/Combination Problems
4. Maze solving
5. N-Queens problem

## Examples
### Generate permutations of a list `[1,2,3]`

```typescript
function permute(nums: number[]): number[] {
	function backtrack(path: number[], used: number[]): void {
		if (path.length == nums.length) {
			result.push([...path]);
			return;
		}
		
		for(let i = 0; i < nums.length; i++) {
			if (!used[i]) {
				used[i] = true;
				path.push(nums[i]);
				backtrack(path, used);
				
				path.pop(); // Undo the last choice
				used[i] = false; // Mark as unused for next iteration
			}
		}
	}

	let result = [];
	let used = new Array(nums.length).fill(false);
	backtrack([], used)
}
```

#### Intuition
- Add current element to path and marked current element as `used`.
- Continue to explore the possibilities of the current element by recursive call
- Undo the path/pop the element & mark as `unused` (backtrack) to explore new possibilites of another element in array
- If path contains all elements of `nums`, we have a solution. Path is complete.
#### Decision tree:
```
Start: []
├── Choose 1 → [1]
│   ├── Choose 2 → [1, 2]
│   │   └── Choose 3 → [1, 2, 3] ✅
│   └── Choose 3 → [1, 3]
│       └── Choose 2 → [1, 3, 2] ✅
├── Choose 2 → [2]
│   ├── Choose 1 → [2, 1]
│   │   └── Choose 3 → [2, 1, 3] ✅
│   └── Choose 3 → [2, 3]
│       └── Choose 1 → [2, 3, 1] ✅
└── Choose 3 → [3]
    ├── Choose 1 → [3, 1]
    │   └── Choose 2 → [3, 1, 2] ✅
    └── Choose 2 → [3, 2]
        └── Choose 1 → [3, 2, 1] ✅
```

### [Combination Sum](https://leetcode.com/problems/combination-sum)

>Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.
>The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

**Input:** candidates = `[2,3,6,7]`, target = 7
**Output:** `[[2,2,3],[7]]`

### Intuition:  
Since the problem allows to reuse an element multiple times, we can backtrack over and over until the remaining target = 0 or less than 0.  
In each backtrack, we decrement the remaining target by `target - candidates[i]`:

- If `remainingTarget == 0` We have find a combination that sum up to `target`
- If `remainingTarget < 0`. We have not found a combination, return to parent and remove element from `path`

**Note**: The problem allow to reuse elements but dont allow to have duplicate combinations: `[2,3,3]` and `[3,2,2]` are the same. So `[2,3,3]` is enough.  
In order to do this, we have to keep track of the `currentIndex` in our backtrack steps, `currentIndex` let us explore new combinations while not producing duplicates by skipping the previous elements.

So our backtrack will look like this:
```javascript
backtrack(path, currentIndex, remainingTarget) {}
```
In each backtrack, we explore combinations by using `for` to loop through `candidates`.  
The loop is started from `currentIndex` to use the same element multiple times and prevent using previous elements.  
At each iteration, we add currentElement to `path` and continue to go deeper. After that, we pop the `path` to try new combinations.