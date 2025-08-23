## MIDDLE-LINKEDLIST
```cpp
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        if (!head || !head->next) return head ;

        ListNode* slow = head ;
        ListNode* fast = head ;
        // even len : stops as fast = null
        // odd len : stops as fast->next = null
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N) | O(N/2) as fast pointer take the leap of +2 & terminated the while loop |
| 🧠 SPACE |    O(1)        |NO extra space |
