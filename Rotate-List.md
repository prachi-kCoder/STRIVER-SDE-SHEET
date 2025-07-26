# ROTATE-LIST

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
    ListNode* rotateRight(ListNode* head, int k) {
        int len =  0;
        if (!head || !head->next) return head ;

        ListNode* temp = head ;
        ListNode* lastNode = nullptr ;
        while (temp) {
            len++ ;
            if (!temp->next) {
                lastNode = temp ;
            }
            temp = temp->next ;
        }
        k %= len ;
        if (k == 0) return head ;

        temp = head ;
        int cnt = 1 ;
        while (cnt < len-k && temp) {
            cnt++ ;
            temp = temp->next ;
        }
        ListNode* newHead = temp->next ;
        temp->next = nullptr ;

        lastNode->next = head ;
        head = newHead ;

        return newHead ;
    }
};
```
# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N + (N-K)) = O(N)     | Len computations , + Traversal upto N-Kth Node for rotation           |
| 🧠 SPACE | O(1)      |    No extra space used         |
