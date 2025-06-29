![[linked-list.png]]

# Definition
Linked list is a chain of nodes that is linked together.
- Singly linked list: Each node has 1 connection to the other node. So, list only has 1 direction, from start to end. List ends when a node points to null.
- Doubly linked list: Each node has 2 connections to other nodes. Which means we can traverse the list both directions, forward and backward.. List ends when both `head.back` = null and `end.next` = null;

# Structure
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

# Traverse 
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

# Common operations
1. Traversal
2. Insertion
3. Deletion
4. Seaching
5. Reversing

# Common techniques
1. Two pointer
	We use 2 pointers `slow` and `fast` to traverse the list to `search`, `reorder`, `delete` with specific requirements. 
		- https://leetcode.com/problems/odd-even-linked-list
		- https://leetcode.com/problems/reverse-linked-list
		- https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list
		- https://leetcode.com/problems/partition-list/