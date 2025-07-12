# Add-Two-Numbers
## INTUITION : Numbers  are reversed but this is the point where people get confused that do they need to reverse the linkedList or not , but no
## as Adding up number requires us to start from the RHS , keeping carry and that is what we have been given as Linked Traversal is such that we traver digits in number from RHS to LHS , just keep the head of the final linked list to return at the end .

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* res = nullptr ;
        ListNode* temp = nullptr ;
        int carry = 0 ;
        
        while (l1 != nullptr || l2 != nullptr) {
            int sum = 0;
            if (l1 != nullptr) sum += l1->val ;
            if (l2 != nullptr) sum += l2->val ;
            sum += carry ; 

            carry = sum/10 ; 
            ListNode* newNode = new ListNode(sum%10) ;
            if (res == nullptr) {
                res = newNode ;
                temp = newNode ;
            } else {
                temp->next = newNode ;
                temp = temp->next;
            }
            if (l1 != nullptr) l1 = l1->next;
            if (l2 != nullptr) l2 = l2->next;
        }
        
        if (carry != 0) {
            temp->next = new ListNode(carry);
            temp = temp->next ;
        }

        return res ;
    }
};
```
## 🧠 Complexity Analysis
| METRIC    | COMPLEXICITY    | HOW  ?  | 
|------------|----------------|----------|
| TIME       | O (max(n,m))   | Traversal will be determined by the longes linked list | 
| SPACE     | O (max(n,m) + 1)   | {Final LL} + 1  , carry for worst case | 
