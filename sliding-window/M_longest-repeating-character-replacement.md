```python
from collections import defaultdict

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        myCounter = defaultdict(int)
        lengthLongest = 0
        mostFreqCharacter = 0
        left = 0    

        for right in range(0, len(s)):
            currCharacter = s[right]
            myCounter[currCharacter] += 1
            mostFreqCharacter = max(mostFreqCharacter, myCounter[currCharacter])
            while ((right - left + 1) - mostFreqCharacter) > k:
                myCounter[s[left]] -= 1
                left += 1
                # mostFreqCharacter = self.getMostFreqCharacter(myCounter)

            lengthLongest = max(lengthLongest, right - left + 1)
    
        return lengthLongest
    

    def getMostFreqCharacter(self, myDict) -> int:
        mostFreqCharacter = 0
        for i in range(ord("A"), ord("Z") + 1):
            mostFreqCharacter = max(mostFreqCharacter, myDict[chr(i)])
        return mostFreqCharacter

```

## NOTE:
- Algorithm works fine if we ommit the recomputation of the most frequent character. TODO: Figure out why this is fine. 
- Space complexity is $O(26)$ because we are storing only the alphabet's keys. 
