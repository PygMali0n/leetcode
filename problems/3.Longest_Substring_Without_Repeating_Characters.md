### key points
- using hash table keep track of most recent repeated character.
- using a starting pointer to save the first index of current substring.
- if find duplicate character then update the starting index with the next index of the previous one

### time complexity
- O(n) (iterate the whole string)
### space complexity
- O(min(m, n)) (distinct character stored in hashmap)

### C++ implementation

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> index_map;
        int start = 0, max_len = 0;
        for (int i = 0; i < s.size(); i++) {
            if (index_map.count(s[i]) == 1 && index_map[s[i]] >= start) {
                start = index_map[s[i]] + 1;
            }
            max_len = max(max_len, i - start + 1);
            index_map[s[i]] = i;
        }
        return max_len;
    }
};

```
