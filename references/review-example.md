# Example: Turning a Data Error into Apparent Success

Request: "Review and fix the function that calculates the average score." Contract: Accept a nonempty list of numbers; otherwise raise ValueError.

Before the fix:

```python
def average_score(scores):
    try:
        return sum(scores) / len(scores)
    except Exception:
        return 0
```

**[P2] Returning zero hides invalid input** - `scores.py:4`.
Evidence: `average_score([])` and `average_score(["bad"])` both return zero even though the contract requires ValueError. Impact: The caller cannot distinguish a valid zero average from invalid data.

Minimal fix:

```python
def average_score(scores):
    if not scores:
        raise ValueError("scores must not be empty")
    try:
        return sum(scores) / len(scores)
    except TypeError as exc:
        raise ValueError("scores must contain numbers") from exc
```

Verification: The average of `[10, 20]` is 15, the average of `[0, 0]` is zero, and empty or nonnumeric inputs raise ValueError. The invalid-input tests fail before the fix and pass afterward.

This is an educational example with an explicit contract, not a claim that an external project contains this defect. The finding's priority may change if its actual impact is greater.
