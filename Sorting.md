# Sorting

## MergeSort
You basically take the ```mid = (l + r) /2``` recursively of each left and right array until there are only 2 elements left in each array/linkedlist.

During each backtracking, you create two list, where you split the array into two sections. Then they are combined into one array by comparing each value from each splitted array into one list

```
ListNode* sortLL(ListNode* left, ListNode* right) {
	ListNode* h = new ListNode(0); //dummy
	ListNode* curr = h;
	while (left != nullptr && right != nullptr) {
		if (left->val <= right->val) {
			curr->next = left;
			left = left->next;
		}
		else {
			curr->next = right;
			right = right->next;
		}
		curr = curr->next;
	}
	while (left != nullptr) {
		curr->next = left;
		curr = curr->next;
		left = left->next;
	}

	while (right != nullptr) {
		curr->next = right;
		curr = curr->next;
		right = right->next;
	}

	return h->next;
}
```
