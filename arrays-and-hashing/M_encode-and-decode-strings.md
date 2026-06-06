**Link:** https://leetcode.com/problems/encode-and-decode-strings/

---

## Problem Translation

We want to design two functions that: a. Encodes a list of strings into a string. and b. Decodes a string into a list of strings. It is important to note that each string given from the original list of strings can contain any possible character out of the 256 valid ASCII characters.

---

## Brute Force Solution

N/A.

---

## Optimal Solution

The naive approach of just using plain delimiters (e.g. `.`) to join strings will break as soon as one of the strings actually contain that delimiter.

We instead use a strategy called: **length-prefix encoding**. Before each string, we write its character count followed by a `#` seperator. For example, `["Hello", "World"]` becomes `"5#hello5#world"`. This way, during decoding we never scan for the end of a word as we know precisely how long each word is. We can thus directly use index arithmetic to obtain the original string. We still need the delimiter `#` because the amount of digitis used to represent the length could be any number with any amount of digits. The `#` functions acts as a terminator for the amount of digits for the length.

`Encode`: concatenate every string into one long string. Each string is first prepended by the length of the string + a `#` delimiter.

`Decode`: We utilize two pointers: i and j. i marks the start of the current length-prefix. j will iterate as long as it doesn't encounter a `#` yet. If it does, this means `s[i:j]` will be the length number for this current string. We then slice exactly `s[i:j]` characters starting at `j+1` because j is currently at `#` and we append it to the `decodedStr` array. We also then make sure to update the `i` pointer to right after this string slice such that it's positioned right at the start of the next string's length-prefix.

---

## Code for Optimal Solution

```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        # important to note that strs[i] contains ANY POSSIBLE character out of 256 valid ASCII characters.
        encodedStr = ""
        for s in strs:
            newStr = str(len(s)) + "#" + s
            encodedStr += newStr
        return encodedStr



    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        # ["Hello","World"]
        # --> ["5#hello5#world"]
        decodedStr = []
        i = 0
        while i < len(s):
            j = i
            while(s[j] != "#"):
                j += 1
            length = int(s[i:j])
            decodedStr.append(s[j+1:j+length+1])
            i = j + length + 1
        return decodedStr


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — A single linear pass over the string / list of strings.
- **Space Complexity:** $O(n)$ — The encoded string and the decoded list together store the same characters that were in the input, plus some small overhead from the length and delimiter characters for each string.

---

## Post-Mortem

- Initially assumed the length for strings was always going to be one digit. This was wrong and it was fixed by using the two-pointer strategy to obtain the actual true length of the strings.
- When encoding/decoding data, do not just rely solely on a plain delimiter, unless we can guarantee that delimiter never exists in the data.
- **Length-prefix** is the standard approach for these type of problems as this way, the decoder can just use index arithmetic to obtain the original string instead of scanning every character.
