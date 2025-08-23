# Majority-Element-II
Approach : `2Pass Approach` 
- It works because for freq > n/3 , so at max 2 elements can have this much freq , (n/3 + extra) + (n/3 + extra) + (n/3 - 2*extra)
- Hence at max 2 majorities , other have freq < n/3
- PASS1 : Record the majorty elements
- PASS2 : Ensure their freq > n/3

 
- This it the logic for 1st pass -> `ORDER MATTERS`

```cpp
if (num == n1) f1++;
else if (num == n2) f2++;
else if (f1 == 0) { n1 = num; f1 = 1; }
else if (f2 == 0) { n2 = num; f2 = 1; }
else { f1--; f2--; }

```
- IF you switch on to consider the f1 == 0 /f2 == 0 then you’re prematurely replacing candidates before checking if the current number matches them,
- THIS IS WRONG ! Because :prioritizes reinforcing existing candidates before replacing them.
 ```cpp
  if (f1 == 0) { n1 = num; f1 = 1; }
  else if (f2 == 0) { n2 = num; f2 = 1; }
  else if (num == n1) f1++;
  else if (num == n2) f2++;
  else { f1--; f2--; }

  ```


Code :
```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int n = nums.size();
        int n1 = 0 ,f1 = 0 ;
        int n2 = 0 ,f2 = 0 ;
        for (int i = 0; i < n ; i++) {
            if (nums[i] == n1) f1++ ;
            else if (nums[i] == n2) f2++ ;
             // check if recorded then look for new appearances 
            else if (f1 == 0) {
                n1 = nums[i] ; f1 = 1 ;
            }else if (f2 == 0) {
                n2 = nums[i] ; f2 = 1 ;
            }
            else {
                // other candidates are reduces the chance of these to be in majority !
                f1--;
                f2--;
            }
        }
        f1 = 0 , f2 = 0;
        for (int i = 0; i < n ; i++) {
            if (nums[i] == n1) f1++ ;
            else if (nums[i] == n2) f2++ ;
        }
        if (f1 > n/3 && f2 > n/3) return {n1 , n2} ;
        else if (f1 > n/3) return {n1} ;
        else if (f2 > n/3) return {n2} ;
        return {};
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)        | 2-Pass           |
| 🧠 SPACE |    O(1)        |       No extra space |
