# heap

## time and space complexity

| name       | complexity                  |
| ---------- | --------------------------- |
| height     | $h = \lg \lfloor n \rfloor$ |
| build_heap | $O(n)$                      |
| max_heap   | $O( \lg n)$                 |
| heap_sort  | $O(n \lg n)$                |

## proof

> Given that all elements in array \( A \) are distinct, in the best case, the running time of HEAPSORT is $\Omega(n \lg n)$.

**Solution:**
Assuming the best-case scenario, leaf nodes can be swapped directly to the top, but non-leaf nodes must bubble up.

Let the number of **leaf nodes** be $\lfloor n/2 \rfloor$.
The depth of the **\( i \)-th node** is $\lfloor \lg i \rfloor$, so the maximum number of swaps to bubble up is equal to the depth of the node.

The total number of swaps for **non-leaf nodes** is:
$$\sum_{ i = 1 } ^ { \lfloor n/2 \rfloor } \lfloor \lg i \rfloor$$

We estimate the lower bound:
$$\sum_{ i = 1 }^{ \lfloor n/2 \rfloor } \lfloor \lg i \rfloor \geqslant \sum_{ i = 1 } ^ { \lfloor n/2 \rfloor }( \lg i-1 ) = \lg ( \lfloor n /2 \rfloor !)- \lfloor n/2 \rfloor = \Omega(n \lg n)$$

From recurrence relation:
$$T(n) = T( \lfloor n / 2 \rfloor ) + \Omega(n \lg n)$$
Thus, we conclude:
$$T(n) = \Omega(n \lg n)$$

## code implement

### binary heap

based it's array index feature give this pseudocode

```cpp
PARENT(i) return i >> 1
LEFT(i) return i << 1
RIGHT(i) return i << 1 | 1
```

### build heap
```
BUILD-MAX-HEAP(A, n)
    A.heap-size = n
    for i = floor(n/2) down to 1
        MAX-HEAPIFY(A, i)
```
```
BUILD-MIN-HEAP(A, n)
    A.heap-size = n
    for i = floor(n/2) down to 1
        MIN-HEAPIFY(A, i)
```
### heap sort
`
HEAPSORT(A, n)
    BUILD-MAX-HEAP(A, n)
    for i = n downto 2
        swap(A[1], A[i])
        A.heap-size = A.heap-size - 1
        MAX-HEAPIFY(A, 1)
`
c++ priority_queue default max_heap

```cpp
priority_queue<int> max_heap;
priority_queue<int, vector<int>, less<int>> max_heap;

priority_queue<int, vector<int>, greater<int>> min_heap;
```

java priority_queue default min_heap

```java
PriorityQueue<Integer> max_heap = new PriorityQueue<Integer>((a, b) -> (b - a));

PriorityQueue<Integer> min_heap = new PriorityQueue<Integer>();
PriorityQueue<Integer> min_heap = new PriorityQueue<Integer>((a, b) -> (a - b))
```

python create heap only min_heap

```python
heapq.heapify(x)
```
