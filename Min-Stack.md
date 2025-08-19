# Min-Stack
- Push: You only push to mn_order if the new value is strictly smaller than the current minimum. This ensures mn_order.back() always points to the index of the current minimum.
- Pop: You check if the popped index is the same as the top of mn_order. If yes, you pop from mn_order too — because the minimum is leaving.
- getMin: Always returns v[mn_order.back()], which is the current minimum in constant time.
  
```cpp
class MinStack {
public:
    vector<int> v ;
    vector<int> mn_order ;
    MinStack() {
    }
    
    void push(int val) {
        v.push_back(val) ;
        int i = v.size()-1 ;
        int sz = mn_order.size()  ;

        if (mn_order.empty()) {
            mn_order.push_back(i);
        }else if (v[mn_order[sz - 1]] > val) {
            mn_order.push_back(i) ; // index of min_val 
        }
    }

    void pop() {
        int i = v.size()-1 ;// most recent !
        v.pop_back();
        int sz = mn_order.size() ;
        if (!mn_order.empty() && mn_order[sz-1] == i) {
            mn_order.pop_back();
        }
    }
    
    int top() {
        return v.empty() ? -1 : v[v.size()-1] ;
    }
    
    int getMin() {
        if (mn_order.empty()) return v[0] ;
        return v[mn_order.back()] ;
    }
};


```
