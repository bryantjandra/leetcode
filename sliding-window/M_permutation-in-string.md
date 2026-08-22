```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        freq_arr_s1 = [0] * 26
        freq_arr_window = [0] * 26


        if len(s2) < len(s1):
            return False


        for i in range(0, len(s1)):
            freq_arr_s1[ord(s1[i]) - ord('a')] += 1
            freq_arr_window[ord(s2[i]) - ord('a')] += 1

        if freq_arr_s1 == freq_arr_window:
                return True

        for right in range(len(s1), len(s2)):
            left = right - len(s1)
            freq_arr_window[ord(s2[right]) - ord('a')] += 1
            freq_arr_window[ord(s2[left]) - ord('a')] -= 1
            # this check is O(26)! because we are comparing two arrays of size 26
            if freq_arr_s1 == freq_arr_window:
                return True
        

        return False

```