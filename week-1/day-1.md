# Prefix Sum + Hash Map – Subarray Sum Equals K

## 🧠 Problem Statement

Given an array of integers `nums` and an integer `k`, return the **number of continuous subarrays** that sum up to `k`.

This is a classic use case for the **Prefix Sum** technique, optimized with a **hash map** to achieve linear time complexity.

## ✅ Core Idea

We want to efficiently find how many subarrays sum to `k`.
g
To do this, we:
1. Maintain a `prefix_sum` while iterating through the array.
2. Track how many times each `prefix_sum` has occurred using a dictionary (`sum_map`).
3. If at any point, `prefix_sum - k` is found in the map, it means:
   - There's a previous subarray that ends just before the current index and has a sum of `k`.


## 🔧 Python Implementation

```python
def subarray_sum(nums: list[int], k: int) -> int:
    count = 0
    prefix_sum = 0
    sum_map = {0: 1}

    for num in nums:
        prefix_sum += num
        count += sum_map.get(prefix_sum - k, 0)
        sum_map[prefix_sum] = sum_map.get(prefix_sum, 0) + 1

    return count
```

## 📊 Example
### Input:
```python
nums = [1, 1, 1]
k = 2
```
### Output:
```python
2
```

### Explanation:

Valid subarrays are:

- `[1, 1]` (at indices 0–1)

- `[1, 1]` (at indices 1–2)

## ⏱️ Time & Space Complexity

- *Time Complexity*: O(n)
- *Space Complexity*: O(n)

## 💡 Why This Works
At every index, we check:
```python
prefix_sum - k
```
If that value has been seen before, the subarray from that earlier index + 1 up to the current index sums to `k`.

We also initialize the map with `{0: 1}` to handle the case where a subarray from index `0` sums to `k`.

