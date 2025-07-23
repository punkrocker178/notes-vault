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
			result.push(path);
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