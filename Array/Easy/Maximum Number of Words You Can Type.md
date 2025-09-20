# Maximum Number of Words You Can Type — Analysis

## 1. Algorithm (in simple English)
1. Convert `brokenLetters` into an `unordered_set<char>` for **O(1) lookup**.  
2. Initialize:
   - `contains` → to track if the current word has any broken letter.  
   - `count` → total number of typeable words.  
3. Iterate over each character in `text`:
   - If the character is in `Broken`, set `contains = true`.  
   - If the character is a space or the **last character** of text **and** `contains == false`, increment `count` (word can be typed).  
   - Reset `contains = false` after encountering a space to start the next word.  
4. Return `count`.  

---

## 2. Code
```cpp
class Solution {
public:
    int canBeTypedWords(string text, string brokenLetters) {
        unordered_set<char> Broken(brokenLetters.begin(), brokenLetters.end());
        bool contains = false;
        int count = 0;

        for(int i = 0; i < text.size(); i++) {
            if(Broken.count(text[i])) {
                contains = true;
            }
            if((text[i] == ' ' && !contains) || (i == text.size() - 1 && !contains)) {
                count++;
                contains = false;
            }
            if(text[i] == ' ') {
                contains = false;
            }
        }

        return count;
    }
};
```

---

## 3. Time Complexity
**O(n + m)**  
- `n = length of text` → iterate once over the text.  
- `m = length of brokenLetters` → building the `unordered_set`.  
- Lookup in the set is O(1) on average.  

---

## 4. Space Complexity
**O(m)**  
- The `unordered_set` stores all broken letters.  
- Constant extra space for counters (`count`, `contains`).  

---

## 5. Assumptions / Constraints
- `text` consists of lowercase English letters and spaces.  
- Words are separated by single spaces, no leading/trailing spaces.  
- `brokenLetters` consists of lowercase letters, no duplicates assumed (but handled safely).  
- Empty `text` returns 0.  

---

## 6. Optimizations (if any)
- Instead of iterating character by character, split `text` into words using a stringstream and check each word against `Broken`.  
  - Could make code more readable, but time complexity remains O(n + m).  
- Early exit: if a broken letter is in a word, skip the rest of that word immediately.  

---

## 7. Edge Cases
Handled:
- Empty `text` → returns 0.  
- `text` with all spaces → returns 0.  
- `brokenLetters` is empty → all words are typeable.  
- Last word without trailing space → still counted correctly.  

Potential issues:
- Non-lowercase letters → current code does not normalize.  
- Multiple consecutive spaces → code resets `contains` correctly, but may count empty words depending on input assumptions.  
