# Maximum Alternating Score After Rearranging

## Problem

Given an integer array `nums`, rearrange its elements in any order to maximize the alternating score:

    score = arr[0]^2 - arr[1]^2 + arr[2]^2 - arr[3]^2 + ...

Return the maximum possible score.

### Examples

| Input                | Output | Note                                   |
|----------------------|--------|----------------------------------------|
| `[1, 2, 3]`          | 12     | `[2,1,3]` -> 4 - 1 + 9 = 12            |
| `[1, -1, 2, -2, 3, -3]` | 16  | `[-3,-1,-2,1,3,2]` -> 9 - 1 + 4 - 1 + 9 - 4 = 16 |

### Constraints

- `1 <= nums.length <= 10^5`
- `-4 * 10^4 <= nums[i] <= 4 * 10^4`

## Approach

1. Signs do not matter because every element is squared, so work with the squares.
2. Sort the squares in ascending order.
3. For length `n`, there are `ceil(n/2)` positive (even-index) slots and `floor(n/2)` negative (odd-index) slots.
4. To maximize the score, put the largest squares in the positive slots and the smallest squares in the negative slots.
5. Answer = (sum of the largest `ceil(n/2)` squares) - (sum of the smallest `floor(n/2)` squares).

## Solution

File: `max_alternating_score.py`

```python
from typing import List

class Solution:
    def maxAlternatingSum(self, nums: List[int]) -> int:
        sq = sorted(x * x for x in nums)
        n = len(sq)
        k = n // 2  # number of subtracted slots
        return sum(sq[k:]) - sum(sq[:k])
```

## Complexity

- **Time:** O(n log n), dominated by sorting.
- **Space:** O(n) for the list of squares.

The maximum answer is about 1.6 * 10^14, which fits in a 64-bit integer (relevant for languages without arbitrary-precision integers).
