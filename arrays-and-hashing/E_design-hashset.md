**Link:** https://leetcode.com/problems/design-hashset/description/

---

## Problem Translation

Design a HashSet without using any built-in libraries

---

## Brute Force Solution

N/A.

---

## Optimal Solution

At it's core, a HashSet is built on top of a standard fixed-sized array. The specific indices of the array are referred to as buckets. When we want to insert any element / key, the HashSet needs to know exactly which bucket to put it in such that it can find it instantly later. It determines this using a hash function.

Since we are storing integers, the most common hash function is just using the module operator: `index = key % length of array`.

However, there is a problem when two different integers are placed in the exact same bucket. For example, 15 and 25 with a HashSet of 10 buckets. Both the keys will be placed in bucket 5. This is referred to as a collision. Thus, we can solve this by having each bucket to store another secondary list instead of just holding a single integer. When a collision occurs, we simply append the new key into the secondary list for that specific bucket. This method is called chaining.

It is important that we check for the existence of the key first whenever we add (to avoid duplicates) and whenever we remove (to avoid deleting elements that do not exist) keys.

---

## Code for Optimal Solution

```python
class MyHashSet:

    def __init__(self):
        ## 10000 is used here as the problem constraints specified only 10^4 operations at most.
        self.buckets = [[] for _ in range(10000)]


    def hash(self, key: int) -> int:
        return key % len(self.buckets)

    def add(self, key: int) -> None:
        if self.contains(key):
            return
        else:
            idx = self.hash(key)
            self.buckets[idx].append(key)


    def remove(self, key: int) -> None:
        if not self.contains(key):
            return
        else:
            idx = self.hash(key)
            self.buckets[idx].remove(key)

    def contains(self, key: int) -> bool:
        idx = self.hash(key)
        bucket = self.buckets[idx]
        for i in range(len(bucket)):
            if bucket[i] == key:
                return True

        return False


# Your MyHashSet object will be instantiated and called as such:
# obj = MyHashSet()
# obj.add(key)
# obj.remove(key)
# param_3 = obj.contains(key)
```

---

## Complexity Analysis

- **Time Complexity:** $O(1)$ — For the average case, because our array has 10,000 buckets and there are at most 10,000 operations, the load factor is <= 1. On average, the secondary list will contain 0 or 1 items, making the search effectively instant. $O(n)$ for the worst case. If every single key evaluates to the exact same bucket, the HashSet degrades into a single massive linked list and searching through it will require checking every single element.
- **Space Complexity:** $O(B + n)$ --> $O(n)$ — B is the number of buckets (10,000) and its a constant so it is ignored. n is the number of unique elements inserted into the secondary lists.

---

## Post-Mortem

- Python list instantiation: When creating an array of empty lists, we must use list comprehension `[[] for i in range(10000)]` and not array multiplication. This is because if we do the latter, Python creates 10000 pointers pointing to the exact same list in memory, so any changes in one bucket will be reflected across all buckets simultaneously.
