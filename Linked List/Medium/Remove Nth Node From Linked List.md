# Remove N-th Node From End of List — Analysis

## 1. Algorithm (in simple English)
1. Create a **dummy node** before the head (helps when removing the first node).  
2. Set two pointers:
   - `p1` starts at the dummy node.  
   - `p2` starts at the real head.  
3. Move `p2` forward `n` steps.  
4. Move both `p1` and `p2` forward together until `p2` reaches the end (`nullptr`).  
   - At this point, `p1` is at the node **just before** the one that should be deleted.  
5. Adjust links: `p1->next = p1->next->next`.  
6. Return the list starting from `dummy->next`.  

---

## 2. Code
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* p1 = new ListNode(0, head);  // dummy node
        ListNode* head2 = p1;                  // keep reference to dummy
        ListNode* p2 = head;

        if (p1->next == nullptr) {
            // list is empty
            return nullptr;
        }

        // Move p2 n steps ahead
        for (int i = 0; i < n; i++) {
            p2 = p2->next;
        }

        // Move both pointers until p2 reaches end
        while (p2 != nullptr) {
            p1 = p1->next;
            p2 = p2->next;
        }

        // Delete the target node
        p1->next = p1->next->next;

        return head2->next;  // skip dummy and return real head
    }
};
```

---

## 3. Time Complexity
**O(L)** where `L` = length of the linked list.  
- Each pointer traverses the list at most once.  

---

## 4. Space Complexity
**O(1)** extra space.  
- Only uses a few pointers (`p1`, `p2`, `head2`).  

---

## 5. Assumptions / Constraints
- `1 <= n <= length of list`.  
- List can have 1 or more nodes.  
- Input list is singly linked.  
- Uses a dummy node to handle edge cases (like removing the first node).  

---

## 6. Optimizations (if any)
- Current code already uses the optimal **two-pointer approach** (single pass).  
- One improvement: free the deleted node explicitly to avoid memory leaks in C++. Example:
  ```cpp
  ListNode* temp = p1->next;
  p1->next = p1->next->next;
  delete temp;
  ```
- The `if (p1->next == nullptr)` check is redundant because constraints guarantee `n` is valid.  

---

## 7. Edge Cases
Handled:
- Removing the first node (`n == length of list`).  
- Removing the last node (`n == 1`).  
- Removing from a middle position.  

Potential issues:
- If `n` is larger than the list length → undefined behavior (assumed not to happen).  
- Memory leak if removed node is not `delete`d (depends on coding environment).  
