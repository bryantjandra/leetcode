**Link:** https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

---

## Problem Translation

We are given an integer array `prices` where each integer symbolizes a price of a stock for that day.

We can only hold at most one share of the stock. On any given day, we can thus buy the stock at that given price, or sell our stock (which we have bought previously) at that given price. Unlike Stock I, we are allowed to make unlimited transactions.

---

## Brute Force Solution

N/A.

---

## Optimal Solution

We utilize a greedy approach. As we iterate through the `prices` array, we keep track of the minimum price seen so far, which represents the price we bought the stock at. Whenever we encounter a price greater than our current minimum, we immediately sell and add the difference to our total profit. We then update our minimum to this new price, ready to buy again if a better opportunity arises.

The greedy choice here is valid because holding out for a higher price later is not gonna be beneficial as any future gain can always be captured in a subsequent transaction (unlimited transactions are allowed). We trust that making the locally optimal choice at each step leads to a globally optimal solution. 

## Code for Optimal Solution

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        currProfit = 0
        minPrice = float("inf")
        for price in prices:
            if price < minPrice:
                minPrice = price
            elif price > minPrice:
                currProfit += price - minPrice
                minPrice = price

        return currProfit
```

---

## Complexity Analysis

- **Time Complexity:** $O(n)$ — Looping through the `prices` array just once.
- **Space Complexity:** $O(1)$ — No auxiliary data structure is used.

---

## Post-Mortem

- The problem differs from **Best Time To Buy & Sell Stock 1**, because unlimited transactions are allowed. This is essentially what makes the greedy approach valid.
