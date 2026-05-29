**Link:** https://leetcode.com/problems/top-k-frequent-elements/

---

## Problem Translation

We want to find the k most frequent elements in an array.

---

## Brute Force Solution

N/A.

## Optimal Solution

We can utilize a HashMap to obtain the counts of each unique element in `nums` array. After that, we utilize a max heap in order to put the most frequent elements at the top.
Then, we can just poll the max heap `k` times in order to obtain the `k` most frequent elements.

---

## Code for Optimal Solution

```python
from collections import defaultdict
import heapq

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = defaultdict(int)
        for num in nums:
            counter[num] += 1
        max_heap = [(-count, num) for num, count in counter.items()]
        heapq.heapify(max_heap)

        res = []
        for i in range(k):
            count, num = heapq.heappop(max_heap)
            res.append(num)

        return res


```

---

## Complexity Analysis

- **Time Complexity:** $O(n log n)$ — Counting the frequencies takes O(n) work. Heapify also takes O(n) work. But each heappop runs in $O(log n)$. Each heappop is also called k times and at worst its called n times. Thus, worst case is when k $\approx$ n.
- **Space Complexity:** $O(n)$ — HashMap and heap each store at most n unique elements.

---

## Post-Mortem

- To transform a minheap in Python into a max heap, we have to negate the number we want to sort by.
- Also, if we pass in a tuple, it'll compare the first element and if ties, then it'll compare the second.
- heapq.heapify(max_heap) to turn a normal array into a heap in-place. This takes $O(n)$ work.
- heapq.heappop(max_heap) to remove and return the smallest element in $O(log n)$ time.
- $O(n)$ solution utilizes a more complex bucket sort algorithm. More details are shown below.

1. Bucket sort works here because the frequency of each unique element is bounded and predictable (each frequencies can only range from 1-n), and thus we can use it as an index. 

2. The values at each index will be a list of the unique numbers in nums array that each have a frequency matching that index!

3. All we then have to do is iterate from the end of our buckets array all the way to the front, and collect elements from every single bucket, up until we have k elements.

```python
from collections import Counter
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = Counter(nums)

        # n+1 buckets (index 0 unused), each bucket is a list
        # since multiple numbers can share the same frequency
        buckets = [[] for _ in range(len(nums) + 1)]

        for num, count in counter.items():
            buckets[count].append(num)

        # read from right to left, collect until we have k elements
        res = []
        for i in range(len(buckets) - 1, 0, -1):
            for num in buckets[i]:
                res.append(num)
                if len(res) == k:
                    return res
```
