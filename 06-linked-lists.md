# Linked Lists :
## Fast and Slow Pointer : 
### To find a cycle :
- Slow pointer moves one step at a time
- Fast pointer moves twice the speed of slow
    - While (fast and slow can advance)
    - Advance fast 2 times
    - Advance slow once
    - If (slow == fast)
        - Cycle exists!
- If we reach here then there is no cycle

### To find the node where the cycle occurred : 
- Slow pointer moves one step at a time
- Fast pointer moves twice the speed of slow
    - While (fast and slow can advance)
    - Advance fast 2 times
    - Advance slow once
    - If (slow == fast)
        - Cycle exists!
- If fast reached the end ⇒ No cycle found
- Otherwise
	- Reset slow to the beginning
	- While (fast != slow)
		- Advance slow 1 step
		- Advance fast 1 step // Reducing hence the speed of fast
	- Return Slow 

**Explanation :**
Once the cycle is detected if we reset slow to the beginning and reduce the speed of slow both pointers will eventually meet at the start of the cycle (At the cycle node)

### Find middle of a linked list :
- Set slow pointer at the beginning
- Set fast pointer two steps after
- While (fast && slow && can advance)
	- Advance slow 1 step
	- Advance fast 2 steps
- When fast reaches the end, Slow will be already in the middle

### Problems
- https://leetcode.com/problems/find-the-duplicate-number/

### In place reversal of linked list : 
**Template (Recursive) :**
```cpp
ListNode* reverseList(ListNode* head) {
    if (head == NULL || head->next == NULL)
                return head;
    ListNode* tempNode = reverseList(head->next);
    head->next->next = head;
    head->next = NULL;
    return tempNode;
}
```