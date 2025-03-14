# heap

## time and space complexity

$h=lg \lfloor n \rfloor$

## addition implement

### binary heap

based it's array index feature give this pseudocode

```cpp
PARENT(i) return i >> 1
LEFT(i) return i << 1
RIGHT(i) return i << 1 | 1
```

### code implement

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
