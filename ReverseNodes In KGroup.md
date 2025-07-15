# REVERSE NODES IN K GROUP
```cpp
class Solution {
public:
    pair<ListNode*,ListNode*> reverse(ListNode* prevofHead,ListNode* head, int k) {
        int len = 0 ;
        ListNode* temp = head ;
        while (temp && len < k) {
            temp = temp->next ;
            len++;
        }
        if (len == k) {
            ListNode* curr = head ;
            ListNode* nxtNode;
            ListNode* prev = prevofHead;
            int cnt = 0 ;
            while (cnt < k && curr) {
                nxtNode = curr->next ;
                curr->next = prev ;
                prev = curr ;
                curr = nxtNode ;
                cnt++ ;
            }
            // curr is not out of K group {nxt to it}
            head->next = curr ;
            return {prev,curr } ;
        }else {
            return {head,nullptr} ;// no change 
        }
    }
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* dummy = new ListNode(0); 
        dummy->next = head ;
        ListNode* curr = head ;
        ListNode* prev = dummy ;

        while (curr) {
            auto p = reverse( prev, curr , k) ;
            ListNode* revHead = p.first ;
            ListNode* nextHead = p.second ;
            if (revHead != curr){
                prev->next = revHead ;
                prev = curr ;
                curr = nextHead ;
                
            }else {
                break ;
            }     
        }
        return dummy->next ;
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(2*N)          |  We traversd the same LL twice : To check the len + reversal for KGroups  |
| 🧠 SPACE |   O(1)          |Pointer adjusted no data structure    |
