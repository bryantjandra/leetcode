```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        freq_arr_t = [0] * 52
        freq_arr_window = [0] * 52
        
        min_window_size = float('inf')
        res = ""

        for letter in t:
            freq_arr_t[self.mapLetterToIndex(letter)] += 1
        
        left = 0
        for right in range(0, len(s)):
            freq_arr_window[self.mapLetterToIndex(s[right])] += 1
            while self.isValidWindow(freq_arr_window, freq_arr_t):
                if (right - left + 1) < min_window_size:
                    min_window_size = right - left + 1
                    res = s[left:right + 1]
                freq_arr_window[self.mapLetterToIndex(s[left])] -= 1
                left += 1


        return res

    def isValidWindow(self, freq_arr_window, freq_arr_t) -> bool:
        for i in range(0, len(freq_arr_t)):
            if freq_arr_window[i] < freq_arr_t[i]:
                return False
        
        return True


    
    
    def mapLetterToIndex(self, letter):
        if (letter >= 'A' and letter <= 'Z'):
            return ord(letter) - ord('A')
        else:
            return ord(letter) - ord('a') + 26
```




## NOTE

- The above solution works and it is $O(n+m)$, but it's $O(52*n + m)$
- Below is how it can be improved using a smarter approach:
    - Two variables are used: (1) need --> contains the amount of distinct characters in `t`. (2) have --> contains the amount of characters satisfied (more than or equal to the frequency for that character in `t`, with the caveat that that character actually exists in `t`) in our sliding window. 



```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        freq_arr_t = [0] * 52
        freq_arr_window = [0] * 52
        
        min_window_size = float('inf')
        res = ""


        need = 0

        for letter in t:
            idx = self.mapLetterToIndex(letter)
            if freq_arr_t[idx] == 0:
                need += 1
            freq_arr_t[idx] += 1
        

        have = 0
        left = 0

        for right in range(0, len(s)):
            idx = self.mapLetterToIndex(s[right])
            freq_arr_window[idx] += 1
            if freq_arr_t[idx] > 0 and freq_arr_window[idx] == freq_arr_t[idx]:
                have += 1
            while have == need:
                if (right - left + 1) < min_window_size:
                    min_window_size = right - left + 1
                    res = s[left:right + 1]
                
                left_idx = self.mapLetterToIndex(s[left])
                freq_arr_window[left_idx] -= 1
                if freq_arr_t[left_idx] > 0 and freq_arr_window[left_idx] < freq_arr_t[left_idx]:
                    have -= 1
                left += 1


        return res

    # we can ommit this O(52) check by using a smart approach! The have and need variables
    # def isValidWindow(self, freq_arr_window, freq_arr_t) -> bool:
    #     for i in range(0, len(freq_arr_t)):
    #         if freq_arr_window[i] < freq_arr_t[i]:
    #             return False
        
    #     return True


    
    
    def mapLetterToIndex(self, letter):
        if (letter >= 'A' and letter <= 'Z'):
            return ord(letter) - ord('A')
        else:
            return ord(letter) - ord('a') + 26
 
```