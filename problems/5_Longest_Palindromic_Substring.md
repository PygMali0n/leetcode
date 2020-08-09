# Method 1: character expansion

## key points
- loop through characters, find longest possible palindromic substring where each character as the center
- can be odd or even length palindrom
- update largest possible length and starting index

## complexity analysis
- time complexity: O(n^2) (expanding takes O(n) time)
- space complexity: O(1)

## C++ implementation
```
class Solution {
public:
    string longestPalindrome(string s) {
        int start = 0;
        int leng = 0;
        for (int i = 0; i < s.size(); i++) {
            int odd = expand(s, i, i);
            int even = expand(s, i, i+1);
            int len = max(odd, even);
            if (len > leng) {
                start = i - (len -1) / 2;
                leng = len;
            }
        }
        return s.substr(start, leng);
    }
    
    int expand(string & s, int start, int end) {
        while (start >= 0 && end < s.size() && s[start] == s[end]) {
            start--;
            end++;
        }
        return end - start - 1;
    }
};
```

# Method 2: dynamic programming

##key points
- save start and end position in 2d array as whether palindromic
- P(i, j) = true only if P(i+1,j-1) = true and s[i] == s[j]
- base case P(i,i) == true and P(i,i+1) = true if s[i] == s[i+1]
- dp memorize previous result

## complexity analysis
- time complexity: O(n^2)
- space complexity: O(n^2) (2d array)

## Python implementation
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        dp = [[False] * n for i in range(n)]
        res = ''
        for i in range(n):
            dp[i][i] = True
            res = s[i]
        for j in range(n-1, -1, -1):
            for k in range(j+1, n):
                if s[j] == s[k]:
                    if k - j == 1 or dp[j+1][k-1]:
                        dp[j][k] = True
                        if len(res) < k - j + 1:
                            res = s[j: k+1]
        return res
 ```

