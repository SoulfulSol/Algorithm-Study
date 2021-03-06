## LeetCode - Longest Substring Without Repeating Characters [Medium]

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

**Example 2:**

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

Link: https://leetcode.com/problems/longest-substring-without-repeating-characters/



---

#### My solution (Java)

  ```
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        int answer = 0;
        for (int i = 0; i < s.length(); i++) {
            Set<Character> set = new HashSet<>();
            int pointer = i;
            int cnt = 0;
            while (pointer < s.length() && !set.contains(s.charAt(pointer))) {
                set.add(s.charAt(pointer));
                cnt++;
                pointer++;
            }
            answer = Math.max(answer, cnt);
        }
        return answer;
    }
}
  ```



---

#### My logic & Feedback

subString 함수를 사용했다간 Time Limit Exceeds 에 바로 걸려버리는 문제.

그래서 그냥 Pointer와 Set을 사용하여 character 하나씩 읽고 set에 저장해가면서 contain 조건에 걸리는 순간의 count를 헤아려

Max값을 return하여 풀었다.



---

#### My solution (Python) - Two pointer, Dictionary 활용

```python
# Two pointer - 20%, 16%

class Solution(object):
    def lengthOfLongestSubstring(self, s):
        res = 0
        p1, p2 = 0, 0
        for i in range(0, len(s)):
            for j in range(p2 - 1, p1 - 1, -1):
                if s[p2] == s[j]:
                    p1 = j + 1
                    break
            res = max(res, p2 - p1 + 1)
            p2 += 1
        return res
```

```
# Dictionary - 95%, 85%

class Solution(object):
    def lengthOfLongestSubstring(self, s):
        p1 = p2 = res = 0
        dic = {}
        while p2 < len(s):
            if s[p2] not in dic:
                dic[s[p2]] = 1
                res = max(res, p2 - p1 + 1)
                p2 += 1
            else:
                del dic[s[p1]]
                p1 += 1
        return res
```

