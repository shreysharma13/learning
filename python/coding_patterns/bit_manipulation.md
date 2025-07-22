# Bit Manipulation Pattern

## What is it?
A technique for solving problems by directly manipulating bits using bitwise operators (AND, OR, XOR, NOT, shifts).

## When to Use
- Problems involving binary representation
- Finding single numbers, subsets, or toggling bits

## Pseudocode
```text
result = 0
for num in nums:
    result ^= num  # XOR to find single number
```

## Classic LeetCode Examples
- [Single Number (LC 136)](https://leetcode.com/problems/single-number/)
- [Counting Bits (LC 338)](https://leetcode.com/problems/counting-bits/)

### Example: Single Number
```python
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num
    return result
```

## Tips
- Use XOR for finding unique elements
- Use bit masks for subset generation

## Mermaid Diagram

```mermaid
flowchart LR
    A["num"] --XOR--> B["result"]
    B --XOR--> C["next num"]
    C --XOR--> D["result"]
``` 