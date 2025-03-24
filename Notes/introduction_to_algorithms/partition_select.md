# Partition Select

## PARTITION-AROUND Algorithm
```sh
PARTITION-AROUND(A, p, r, x)
    ixl = ⌊(p + r) / 2⌋
    ixr = ⌈(p + r) / 2⌉
    half = ⌊(r - p) / 2⌋
    for radius = 0 to half
        if (A[ixl - radius] == x)
            exchange A[r] with A[ixl - radius]
            break
        else if (A[ixr + radius] == x)
            exchange A[r] with A[ixr + radius]
            break
    i = p - 1
    for j = p to r - 1
        if A[j] ≤ x
            i = i + 1
            exchange A[i] with A[j]
    exchange A[i + 1] with A[r]
```

## SELECT Algorithm
```sh
SELECT(A, p, r, i)
    while (r - p + 1) mod 5 ≠ 0
        for j = p + 1 to r  // put the minimum into A[p]
            if A[p] > A[j]
                exchange A[p] with A[j]
        // If we want the minimum of A[p : r], we're done.
        if i == 1
            return A[p]
        // Otherwise, we want the (i - 1)st element of A[p + 1 : r]
        p = p + 1
        i = i - 1
    g = (r - p + 1) / 5  // number of 5-element groups
    for j = p to p + g - 1
        sort ⟨A[j], A[j + g], A[j + 2g], A[j + 3g], A[j + 4g]⟩ in place
    // All group medians now lie in the middle fifth of A[p : r].
    // Find the pivot x recursively as the median of the group medians.
    x = SELECT(A, p + 2g, p + 3g - 1, ⌈g / 2⌉)
    q = PARTITION-AROUND(A, p, r, x)  // partition around the pivot x
    // The rest is just like lines 3-9 of RANDOMIZED_SELECT.
    k = q - p + 1
    if i == k
        return A[q]  // the pivot value is the answer
    else if i < k
        return SELECT(A, p, q - 1, i)
    else return SELECT(A, q + 1, r, i - k)
   return i + 1  // new index of pivot
```

## Proof of Complexity
Let \( T(n) \) be the worst-case runtime of SELECT for an input array \( A[p:r] \), where \( r - p + 1 \leq n \).

### Step 1: Analyzing Non-Recursive Steps
- The `while` loop (lines 1-10) runs 0 to 4 times, taking \( O(1) \).
- The minimum search (lines 2-4) dominates, taking \( \Theta(n) \), making lines 1-10 run in \( O(n) \cdot \Theta(1) = O(n) \).
- Sorting 5-element groups (lines 12-13) takes \( \Theta(n) \).
- PARTITION-AROUND (line 17) runs in \( \Theta(n) \).
- Total time: \( O(n) + \Theta(n) + \Theta(n) + \Theta(1) = \Theta(n) \).

### Step 2: Analyzing Recursive Steps
- \( g \leq n/5 \), so the recursive pivot selection (line 16) takes \( T(g) \leq T(n/5) \).
- The partition step ensures that at most \( 7n/10 \) elements remain after partitioning.
- Recurrence relation:
  \[
  T(n) \leq T(n/5) + T(7n/10) + \Theta(n)
  \]

Using substitution, we assume \( T(n) = O(n) \), which holds since the constants balance out, proving \( T(n) = \Theta(n) \).

### Comparison with Comparison-Based Sorting
- **Similarity**: Both use comparisons to determine element order.
- **Difference**: Comparison sorts fully order the array with a lower bound of \( \Omega(n \log n) \), while SELECT solves the selection problem in \( \Theta(n) \) without full sorting.

## Additional Resources
- [Median of Medians Algorithm](https://gist.github.com/boulethao/a15809963d326a5ad43f255fbffbf9ff)

