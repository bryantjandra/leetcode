**Link:** https://leetcode.com/problems/design-hashmap/description/

---

## Problem Translation

Design a HashMap without using any built-in libraries.

---

## Brute Force Solution

N/A.

---

## Optimal Solution

This is similar to the `Design Hashset` problem. Again a HashMap is built on top of a standard fixed-size array. The specific indices of the array are referred to as buckets. When we want to insert any key-value pair, the HashMap needs to know which bucket to put it in such that it can find it instantly later. We use a hash function for this.

The hash function we use here is: `index = key % length of array`.

Whenever two different key-value pairs are placed in the exact same bucket (collision), we solve this by having each bucket store secondary lists instead of just holding a single integer. Thus, each bucket holds a secondary list of key-value pairs (stored as two-element lists).

During insertion, we iterate through the bucket. If the key already exists, we update its associated value. If we finish the scan of the entire bucket and the key is not found, we append this new key-value pair to the bucket.

---

## Code for Optimal Solution

```python
class MyHashMap:

    def __init__(self):
        self.buckets = [[] for i in range(10000)]

    def hash(self, key: int) -> int:
        return key % len(self.buckets)

    def put(self, key: int, value: int) -> None:
        idx = self.hash(key)
        bucket = self.buckets[idx]
        for pair in bucket:
            if pair[0] == key:
                pair[1] = value
                return
        bucket.append([key, value])

    def get(self, key: int) -> int:
        idx = self.hash(key)
        bucket = self.buckets[idx]
        for pair in bucket:
            if pair[0] == key:
                return pair[1]
        return -1


    def remove(self, key: int) -> None:
        idx = self.hash(key)
        bucket = self.buckets[idx]
        for pair in bucket:
            if pair[0] == key:
                bucket.remove(pair)
                return


# Your MyHashMap object will be instantiated and called as such:
# obj = MyHashMap()
# obj.put(key,value)
# param_2 = obj.get(key)
# obj.remove(key)
```

---

## Complexity Analysis

- **Time Complexity:** $O(1)$ — For the average case, because our array has 10,000 buckets and there are at most 10,000 operations, the load factor is <= 1. On average, the secondary list will contain 0 or 1 items, making the search effectively instant. $O(n)$ for the worst case. If every single key evaluates to the exact same bucket, the HashMap degrades into a single massive linked list and searching through it will require checking every single element.
- **Space Complexity:** $O(B + n)$ --> $O(n)$ — B is the number of buckets (10,000) and its a constant so it is ignored. n is the number of unique key-value pairs inserted into the secondary lists.

---

## Post-Mortem

N/A
