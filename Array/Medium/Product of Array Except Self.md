# Product of Array Except Self — Analysis

## 1. Algorithm (in simple English)
1. Initialize two arrays, `prefix` and `suffix`, both of size `n` (number of elements), filled with `1`.  
   - `prefix[i]` will store the product of all elements **before** index `i`.  
   - `suffix[i]` will store the product of all elements **after** index `i`.  
2. Fill the `prefix` array from left to right:
   - `prefix[i] = prefix[i-1] * nums[i-1]`.  
3. Fill the `suffix` array from right to left:
   - `suffix[j] = suffix[j+1] * nums[j+1]`.  
4. Multiply `prefix[i] * suffix[i]` for each index `i` to get the final result.  
5. Return the result array.  

---

## 2. Code
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> result;
        vector<int> prefix(nums.size(), 1);
        vector<int> suffix(nums.size(), 1);
        int j = nums.size() - 2;

        for(int i = 1; i < nums.size(); i++) {
            prefix[i] = prefix[i - 1] * nums[i - 1];
            suffix[j] = suffix[j + 1] * nums[j + 1];
            j--;
        }

        for(int i = 0; i < nums.size(); i++) {
            result.push_back(prefix[i] * suffix[i]);
        }

        return result;
    }
};
```

---

## 3. Time Complexity
**O(n)**  
- Each of the three loops runs **once over the array of length n**.  
- No nested loops → linear time.

---

## 4. Space Complexity
**O(n)** extra space  
- Two additional arrays `prefix` and `suffix` of size `n` are used.  
- Result array also uses `O(n)` space, but that is required for output.

> ⚡ Note: Can be optimized to **O(1) extra space** (ignoring output) by storing prefix products in `result` and updating with suffix product on the fly.

---

## 5. Assumptions / Constraints
- `nums` has at least 1 element.  
- Elements may include zero.  
- No division is used (so safe for zeros).  
- Standard 32/64-bit integer overflow is assumed not to occur.

---

## 6. Optimizations (if any)
- Reduce space complexity to O(1) extra space:
  - Store prefix products directly in `result`.  
  - Maintain a single variable `suffix` to multiply on the fly while traversing from the end.  
- This avoids using the `suffix` array entirely.

---

## 7. Edge Cases
Handled:
- Single element array → returns `[1]`.  
- Array containing zeros → handled correctly, zeros will nullify products as expected.  
- Multiple zeros → all positions except zeros may become zero.  

Potential issues:
- Integer overflow if array has very large numbers (depending on constraints).  
- Empty input array → currently returns empty vector (depends if allowed by problem).  
