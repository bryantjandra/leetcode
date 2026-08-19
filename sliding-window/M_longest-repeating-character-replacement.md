```python
from collections import defaultdict

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        left = 0
        res = 0
        my_counter = defaultdict(int)
        most_freq_character_count = 0

        for right in range(0, len(s)):
            curr_character = s[right]
            my_counter[curr_character] += 1
            most_freq_character_count = max(most_freq_character_count, my_counter[curr_character])
            
            while (right - left + 1) - most_freq_character_count > k:
                my_counter[s[left]] -= 1
                left += 1
                # most_freq_character_count = self.getMostFreq(my_counter)
            
            res = max(res, right - left + 1)
        
        return res

    
    def getMostFreq(self, my_counter) -> int:
        most_freq_character_count = 0
        for i in range(ord('A'), ord('Z') + 1):
            most_freq_character_count = max(most_freq_character_count, my_counter[chr(i)])
        
        return most_freq_character_count

```

## NOTE:
- Algorithm works fine if we ommit the recomputation of the most frequent character. Because, never decreasing the most frequent character count --> will never yields a wrong answer. 
- Space complexity is $O(26)$ because we are storing only the alphabet's keys. 
- Stick with the intuitive solution with time complexity of $O(26*n)$ to be safe.
