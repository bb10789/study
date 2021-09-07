# LinkedList
## Recursive and backtrack is your best buddy!!!!!!!

- **Reverse a Singly Linked List**  
Quite Simple, you basically recursive through the entire array first and reversed elements will be returned   
at every backtrack, you do ``` head ->next ->next = head  ``` because you know the next item must be the item right in front of you, since there's two copies of the elements of your ->next, you can append it after that element and it will show up as the returned list.  
```
ListNode* reverseList(ListNode* head) {
	if (head == nullptr || head->next == nullptr) return head;
	ListNode* start = reverseList(head->next);
	head->next->next = head;
    head->next = nullptr;
	return start;
}
```
- Remove Duplicates from a Linked List
  should be pretty easy, at each element, you keep looping `while(curr->next->val == curr->val)`, reset curr->next everytime
- Delete All Occurrences of a Given Key in a Linked List  
bruh
- Sort Linked List Using Insertion Sort   
recursive `	ListNode* list = insertionSortList(head->next);` and backtrack check if it's smaller than head, else, find the element that's larger through while loop
- Intersection Point of Two Lists   
Count the length of both linkedlist, because we know that they end at the the same length, we increment->next
- **Find n'th Node from the End of a Linked List**  
keep track of a pre, and only increment a second pointer when `index++ >= n + 1`, if the index is the same as the size of n, u move the head, otherwise, find it using pre
- Swap Nth Node with Head
recursive and backtrack
```
ListNode* swapPairs(ListNode* head) {
	if (head == nullptr || head->next == nullptr) {
		return head;
	}
	ListNode* h = swapPairs(head->next->next);
	ListNode* newHead = head->next;
	head->next = h;
	newHead->next = head;
	return newHead;
}
```
- Merge Two Sorted Linked Lists
for each element, just check which one is bigger, and append the end with whatever element is left using ->next
- Rotate a Linked List  
  No trick, just find the total size of linkedlist and find the location of index - k, set that to head and
  **remember, curr->next = nullptr**
- Reverse Alternate K Nodes in a Singly Linked List   
1. Two solutions, either recursively do it by finding the section of list, and set the `end->next` to nullptr
send that to a reverse helper and merge them together.  
2. You can do it iteraitively by using a pre pointer that creates a dummy node in the front of the Linkedlist, and then update pre->next to the newest element so `nxt->next = pre->next; pre->next = nxt->next;`

### recursive
```
ListNode* reverseGroupHelper(ListNode* head) {
	if (!head || !head->next) return head;
	ListNode* h = reverseGroupHelper(head->next);
	head->next->next = head;
	head->next = nullptr;
	return h;
}

ListNode* reverseKGroup(ListNode* head, int k) {
	if (!head) return head;
	ListNode* curr = head;
	int index = 0;
	ListNode* pre = nullptr;
	for (int i = 0; i < k && curr != nullptr; i++) {
		index++;
		pre = curr;
		curr = curr->next;
	}
	if (index != k) {
		return head;
	}
	ListNode* nextNode = reverseKGroup(curr, k);
	pre->next = nullptr;
	ListNode* reverse = reverseGroupHelper(head);
	head->next = nextNode;
	return reverse;
}
```
iteraitively
```
ListNode* reverseKGroup2(ListNode* head, int k) {
	if (!head || !head->next) return head;
	ListNode* preheader = new ListNode(-1);
	preheader->next = head;
	ListNode* curr = head, * nxt, * pre = preheader;
	int num = 0;
	while (curr = curr->next) num++;
	while (num >= k) {
		curr = pre->next;
		for (int i = 1; i < k; i++) {
			nxt = curr->next;
			curr->next = nxt->next;
			nxt->next = pre->next;
			pre->next = nxt;
		}
		pre = curr;
		num -= k;
	}
	head = preheader->next;
	delete preheader;
	return head;
}
```
- Add Two Integers Represented by Linked Lists  
just add until there's nothing left, add a new node to the end if there's a carry
- Copy Linked List with Arbitrary Pointer   
this one is fun, at each node, set the next one as a copy of itself, and then copy the random first by doing
`curr->next->random = curr->random ? curr->random->next : nullptr`
