![[img/linked-list.png]]

## Definition
Linked list is a chain of nodes that is linked together.
- Singly linked list: Each node has 1 connection to the other node. So, list only has 1 direction, from start to end. List ends when a node points to null.
- Doubly linked list: Each node has 2 connections to other nodes. Which means we can traverse the list both directions, forward and backward.. List ends when both `head.back` = null and `end.next` = null;

## Structure
```typescript
class ListNode {
	public val: number;
	public next: ListNode | null;
	constructor(val: number, next?: ListNode) {
		this.val = val ?? -1;
		this.next = next ?? null;
	}
}

// 1->3->4->5->9
let head = new ListNode(1);
head.next = new ListNode(3);
head.next.next = new ListNode(4);
head.next.next.next = new ListNode(5);
head.next.next.next.next = new ListNode(9);
```

## Traversing
We can traverse the list by setting the pointer to be the next node
`head = head.next`

Then we can put in a while loop to iterate until the list ends
```typescript
while(head != null) {
	head = head.next;
}
```

However, rule of thumb is we need to keep the `head` pointer untouched, if we iterate using `head` pointer, we will get `head` = null after the loop ends.
Instead, we should use another pointer.
```typescript
let curr = head;
while(curr != null) {
	// Example: some update operations when we traverse
	// curr.val = 0;
	// move to the next node
	curr = curr.next;
}

// Here we can return the modified list
return head;
```

## Common operations
1. Traversal
2. Insertion
3. Deletion
4. Seaching
5. Reversing

## Common techniques
1. **Two pointers**: O(n) time, O(1) space
	Iteration method. We use 2 pointers `slow` and `fast` to traverse the list to `search`, `reorder`, `delete` with specific requirements. Each problem have different setup between pointers. 
		- [Odd even list](https://leetcode.com/problems/odd-even-linked-list) (odd pointer and even pointer. Each pointer skip 1 node, after iteration end, combine both list to return result)
		- [Reverse linked list](https://leetcode.com/problems/reverse-linked-list) (3 pointers to increase readability: `prev`, `curr`, `next`. At each iteration, we set the relations of `curr` and `prev`, then move 3 pointers forward)
		- [Delete the middle node of a linked list](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list) (`fast` and `slow` pointer, `fast` is always 2 steps ahead of slow. Which is double the movement of `slow`. By the time `fast` is null, `slow` is at the middle)
		- [Remove nth node from end of list](https://leetcode.com/problems/remove-nth-node-from-end-of-list) (`fast` and `slow`. We can initially move `fast` by `k` steps ahead of `slow`. If `fast` = null then  `slow` has reached the node)
		- [Partitrion list](https://leetcode.com/problems/partition-list ) (Search problem. Have 2 pointers and 2 dummy nodes. `currBig` and `currSmall`. If `node.val` >= `x`, set relation of pointer `currBig` to node, else set pointer `currSmall` to node. At the end of list iteration, combine both list `small` and `big` to return result) ^f68fef
2. **Dummy / Sentinnel node**
	This technique will append a dummy node to the front of the `head`. By doing this, we have preserved the list, `head` can be used to traverse the list. Also, we can handle edge case like `head` = null gracefully without using if. This technique is usually combined with 2 pointer technique
3. **Recursion**: O(n) time, O(1) space.
	Traverse the list by recursively calling the function with `head.next`. This technique is useful in situations when we need to process from the end of the list. So, problems using this technique is less than 2 pointers.
4. **Create new node**
	Unlike sentinnel node has linked to the actual `head`. This technique is about creating a new `head` that has no relations. At each iteration, we just create a new node and set relation to the `curr` pointer. This technique is make the **solution more straightforward** but the **drawback** is the space complexity is **O(n) extra space**.

# Notable problems
1. [Linked list cycle](https://leetcode.com/problems/linked-list-cycle) (Can use hash map to check visited node. Or, use `fast` and `slow` pointer. `fast` is 2 steps ahead of `slow`, eventually `fast` will meet `slow` at some point so list does have cycle. If not, list doesnt' have cycle)
2. [Merge 2 sorted list](https://leetcode.com/problems/merge-two-sorted-lists) (Can use recursion. My solution is to directly set the relations of 2 list pointing to each other nodes. But this logic is hard to read and feels very hacky. The proper way is to using dummy node then iterate both list. Check the condition and move the pointers at each iteration.)
3. [Copy list with random pointer](https://leetcode.com/problems/copy-list-with-random-pointer/) (Use hashmap to store nodes of the new list, then set `random` from new list to get nodes from map)
4. [Rotate list](https://leetcode.com/problems/rotate-list) (Iterate list to form a cycle, then calculate the new `head` of the list by using `n - (k % n)`. Since the new `tail` before the new `head`  then the formular will need to subtract 1 `n - (k%n) - 1`. After we get the tail, then set the `tail.next` to be null to break the cycle.