# Sri Lanka 12-Digit NIC Check-Digit Validation

A Python toolkit and mathematical specification for calculating and validating the 12th check digit (`C`) in Sri Lanka's National Identity Card (NIC) system (`YYYY DDD SSSS C`).

---

## Mathematical Model

The 12th digit is an integrity check digit generated via a weighted Modulo-11 algorithm over $\mathbb{GF}(11)$. 

Given an 11-digit prefix $d_1, d_2, \dots, d_{11}$ and the positional weight vector $\mathbf{w} = [8, 4, 3, 2, 7, 6, 5, 8, 4, 3, 2]$:

1. **Weighted Sum ($S$):**
   $$S = \sum_{i=1}^{11} w_i d_i$$

2. **Check Digit ($C$):**
   $$C = \Bigl(\bigl(11 - (S \bmod 11)\bigr) \bmod 11\Bigr) \bmod 10$$
   *(Note: The outer modulo $10$ folds any internal remainder of $10$ down to $0$).*

---

## Python Function

```python
def get_nic_check_digit(prefix_11: str) -> int:
    """Calculates the 12th check digit (C) for an 11-digit Sri Lankan NIC prefix."""
    weights = [8, 4, 3, 2, 7, 6, 5, 8, 4, 3, 2]
    weighted_sum = sum(int(digit) * weight for digit, weight in zip(prefix_11, weights))
    return ((11 - (weighted_sum % 11)) % 11) % 10