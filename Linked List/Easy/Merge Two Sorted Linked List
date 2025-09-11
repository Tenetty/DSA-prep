---

# Merge Two Sorted Linked Lists — Analysis

## 1. Algorithm (in simple English)

1. If either list is empty, return the other list immediately.
2. Compare the first nodes of both lists. Whichever has the smaller (or equal) value becomes the **head** of the merged list.
3. Keep an iterator pointer (`iter`) that builds the merged list step by step.
4. While both lists still have nodes:

   * Compare current nodes.
   * Attach the smaller one to `iter->next`.
   * Advance the pointer (`list1` or `list2`) from which the node was taken.
   * Move `iter` forward.
5. When one list becomes empty, attach the remainder of the other list to `iter->next`.
6. Return the merged list starting at `head`.

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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode *head;
        if(list1==nullptr){
            return list2;
        }
        else if(list2==nullptr){
            return list1;
        }
        if(list1==nullptr && list2==nullptr){
            return list1;
        }
        if(list1->val<=list2->val){
            head=list1;
            list1 =list1->next;
        }
        else{
            head=list2;
            list2 = list2 ->next;
        }
        ListNode* iter =head;
        while(list1!=nullptr && list2!=nullptr){
            if(list1->val<=list2->val){
                iter->next = list1;
                list1= list1->next;
                iter =iter->next;
            }
            else{
                iter->next = list2;
                list2= list2->next;
                iter =iter->next;
            }
        }
        if(list1==nullptr){
            iter ->next = list2;
        }
        else{
            iter->next = list1;
        }
        return head;
    }
};
```

---

## 3. Time Complexity

**O(n + m)**

* Each node from `list1` and `list2` is visited and linked exactly once.
* No nested loops; just linear traversal.

---

## 4. Space Complexity

**O(1)** extra space.

* Only a few pointers (`head`, `iter`) are used.
* The function reuses existing nodes instead of creating new ones.

---

## 5. Assumptions / Constraints

* Both input lists are sorted in **non-decreasing order**.
* Lists are singly linked (`ListNode*`).
* Inputs may be `nullptr` (empty list).
* The merge is done **in-place**: original node ordering is modified.

---

## 6. Optimizations (if any)

* The condition `if(list1==nullptr && list2==nullptr)` is redundant because the earlier `if`/`else if` already cover it.
* Can be simplified using a **dummy node** approach, which avoids special handling for the head node and makes the code shorter.
* Recursive solution possible but uses O(n+m) stack space, while this iterative version is more memory-efficient.

---

## 7. Edge Cases

Handled:

* `list1` is empty → returns `list2`.
* `list2` is empty → returns `list1`.
* Both lists empty → returns `nullptr`.
* Duplicate values → keeps all, order stable (nodes from `list1` picked first when equal).

Potential issues if assumptions break:

* If input lists are **not sorted**, the result won’t be sorted.
* If the two lists share nodes (not independent), re-linking may corrupt the structure.
* Very large lists are fine here (iterative avoids recursion depth issues).

---
