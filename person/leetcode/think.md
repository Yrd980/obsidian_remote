# hot100

## hash

### groupAnagrams

1. data structure use Stringbuilder::new Stringbuilder::appendCodePoint Stringbuilder::append

```java

    public static List<List<String>> groupAnagrams(String[] strs) {
       return new ArrayList<>(
           Arrays.stream(strs).collect(Collectors.groupingBy(
             str -> {
                return str.chars().sorted().collect(
                    StringBuilder::new,
                    StringBuilder::appendCodePoint,
                    StringBuilder::append
          ).toString();
        })) .values()
    );
   }
```

### longestConsecutive

1. use set dataset
2. analyse is set.contains() run O(1) time complexity
3. contains(num-1) is the sequence head aka consecutive

```java

  public static int longestConsecutive(int[] nums) {
    Set<Integer> num_set = new HashSet<>();
    for(int num : nums) {
      num_set.add(num);
    }
    int longestStreak= 0;
    for(int num : num_set) {
      if(!num_set.contains(num-1)){
        int currentNum = num;
        int currentStreak = 1;
        while(num_set.contains(currentNum+1)){
          currentNum++;
          currentStreak++;
        }
      longestStreak = Math.max(longestStreak,currentStreak);
      }
    }
    return longestStreak;
  }

```

### twosum

1. this problem involves a single loop. Then condition for judgment is _map.containsKey()_. There is no _else_ statement; instead,it directly uses map.put();

```java

    public static int[] twoSum(int[] nums, int target) {
      Map<Integer,Integer> map = new HashMap<>();
      for(int i = 0 ; i < nums.length ; i++) {
          int complement = target - nums[i];
          if(map.containsKey(complement)){
              return new int[] {map.get(complement),i};
          }
          map.put(nums[i],i);
    }
    throw new IllegalArgumentException("No two sum solution");
    }

```

## twopointer

### moveZeros

1. two point mean fast and slow pointers
2. in this case we use j as slow pointer and for loop  i variable fast
3. then we use

```java
int tmp = nums[i]
nums[i] = nums[j]
nums[j++] = tmp
```

!> [!IMPORTANT]
> just one loop
> if condition nums[i] != 0

```java

  public static void moveZeroes(int[] nums) {
    if (nums == null) {
      return;
    }
    int j = 0;
    for (int i = 0; i < nums.length; ++i) {
      if (nums[i] != 0) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j++] = tmp;
      }
    }
  }

```

### maxArea

1. consider bound condition so we use l = 0; r = height.length - 1;
2. trick use while (l<r)
3. if condition use (height[l]<=height[r]) ++l --r

```java

  public static int maxArea(int[] height) {
    int l = 0, r = height.length - 1;
    int ans = 0;
    while (l < r) {
      int area = Math.min(height[l], height[r]) * (r - l);
      ans = Math.max(ans, area);
      if (height[l] <= height[r]) {
        ++l;
      } else {
        --r;
      }
    }
    return ans;
  }

```

### threeSum

1. not set but Arrays.sort;
2. based condition 1 use target = -nums[first]
3. bound condition first = 0 and nums[first] == nums[first-1] use continue
4. while use two < third set --third

```java

  public static int trap(int[] height) {
    int ans = 0;
    int l = 0, r = height.length - 1;
    int lMax = 0;
    int rMax = 0;
    while (l < r) {
      lMax = Math.max(lMax, height[l]);
      rMax = Math.max(rMax, height[r]);
      if (height[l] < height[r]) {
        ans += lMax - height[l];
        l++;
      } else {
        ans += rMax - height[r];
        r--;
      }
    }
    return ans;
  }

```

### trap

1. use lMax rMax for get "altitude"
2. while loop condition is l < r
3. move pointer base height`[l]` < height`[r]`

```java

  public static int trap(int[] height) {
    int ans = 0;
    int l = 0, r = height.length - 1;
    int lMax = 0;
    int rMax = 0;
    while (l < r) {
      lMax = Math.max(lMax, height[l]);
      rMax = Math.max(rMax, height[r]);
      if (height[l] < height[r]) {
        ans += lMax - height[l];
        l++;
      } else {
        ans += rMax - height[r];
        r--;
      }
    }
    return ans;
  }

	```

## slideWindow

### lengthofLongestSubstring

1. data structure use set
2. assign right pointer r = -1
3. if i!=0 occ.remove(s.charAt(i-1)) move slideWindow
4. then while loop r + 1 < n 

```java
  public int lengthOfLongestSubstring(String s) {
    Set<Character> occ = new HashSet<>();
    int n = s.length();
    int r = -1, ans = 0;
    for (int i = 0; i < n; i++) {
      if (i != 0) {
        occ.remove(s.charAt(i - 1));
      }
      while (r + 1 < n && !occ.contains(s.charAt(r + 1))) {
        occ.add(s.charAt(r + 1));
        r++;
      }
      ans = Math.max(ans, r - i + 1);
    }
    return ans;
  }


```

### findAnagrams

5. use differ for saving memory
6. still initial
7. for loop core mind is move left element aka count-- judge count==0 differ-- move right element aka count++ in a similar way

```java

  public static int indice(String s, int i) {
    return s.charAt(i) - 'a';
  }

  public static List<Integer> findAnagrams(String s, String p) {
    List<Integer> ans = new ArrayList<>();
    int len_s = s.length();
    int len_p = p.length();
    if (s == null || p == null || len_s < len_p)
      return ans;
    int[] count = new int[26];
    for (int i = 0; i < p.length(); i++) {
      count[indice(s, i)]++;
      count[indice(p, i)]--;
    }
    int differ = 0;
    for (int i = 0; i < 26; i++) {
      if (count[i] != 0) {
        differ++;
      }
    }

    if (differ == 0) {
      ans.add(0);
    }

    for (int i = 0; i < len_s - len_p; i++) {
      int indice_l = indice(s, i);
      count[indice_l]--;
      if (count[indice_l] == 0) {
        differ--;
      } else if (count[indice_l] == -1) {
        differ++;
      }
      int indice_r = indice(s, i + len_p);
      count[indice_r]++;
      if (count[indice_r] == 0) {
        differ--;
      } else if (count[indice_r] == 1) {
        differ++;
      }
      if (differ == 0) {
        ans.add(i + 1);
      }
    }
    return ans;
  }

  public static List<Integer> findAnagrams1(String s, String p) {
    int[] ori = new int[26];
    int[] window = new int[26];
    List<Integer> ans = new ArrayList<>();
    for (int i = 0; i < p.length(); i++) {
      ori[p.charAt(i) - 'a']++;
      window[s.charAt(i) - 'a']++;
    }

    if (Arrays.equals(ori, window)) {
      ans.add(0);
    }

    for (int i = 0; i < s.length() - p.length(); i++) {
      window[s.charAt(i) - 'a']--;
      window[s.charAt(i + p.length()) - 'a']++;
      if (Arrays.equals(ori, window)) {
        ans.add(i + 1);
      }
    }
    return ans;
  }
```

## substring

8. use two loop second condition is --end;
9. before i think j pointer is necessary while loop for finding
cur+nums[j] == k but test cases show the 0 is essential but it
cannot work
10. second solution use prefix sum which mean find pre-k

```java

  public static int subarraySum(int[] nums,int k){
    int count = 0;
    int pre = 0;
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0,1);
    for(int i=0; i<nums.length; i++){
      pre+=nums[i];
      if(map.containsKey(pre-k)){
        count+=map.get(pre-k);
      }
      map.put(pre,map.getOrDefault(pre,0)+1);
    }
    return count;
  }

```

### maxSlidingWindow

11. use PriorityQueue
12. use Deque
13. use prefix and suffix slide window use i%k

involve(internal use specify sort algorithm)

```java
PriorityQueue

Comparator default small to big
add : offer
getmax: peek
remove: poll

Deque

Deque interface implement LinkedList

while(!deque.isEmpty() && nums[i]>=nums[deque.peekLast()]){
    deque.pollLast();
}
deque.offerLast(i);

getmax: peekFirst
remove: pollFirst
add: offerLast

```

```java

  public static int[] maxSlidingWindow(int[] nums, int k) {
    if (nums == null || nums.length == 0) {
      return new int[0];
    }

    int n = nums.length;
    PriorityQueue<int[]> pq = new PriorityQueue<>(new Comparator<int[]>() {
      public int compare(int[] pair1, int[] pair2) {
        return pair1[0] != pair2[0] ? pair2[0] - pair1[0] : pair2[1] - pair1[1];
      }
    });

    for (int i = 0; i < k; i++) {
      pq.offer(new int[] { nums[i], i });
    }
    int[] ans = new int[n - k + 1];
    ans[0] = pq.peek()[0];
    for (int i = k; i < n; i++) {
      pq.offer(new int[] { nums[i], i });
      while (pq.peek()[1] <= i - k) {
        pq.poll();
      }
      ans[i - k + 1] = pq.peek()[0];
    }
    return ans;
  }

  public static int[] maxSlidingWindow1(int[] nums, int k) {
    int n = nums.length;
    Deque<Integer> deque = new LinkedList<>();
    for (int i = 0; i < k; i++) {
      while (!deque.isEmpty() && nums[i] >= nums[deque.peekLast()]) {
        deque.pollLast();
      }
      deque.offerLast(i);
    }

    int[] ans = new int[n - k + 1];
    ans[0] = nums[deque.peekFirst()];
    for (int i = k; i < n; i++) {
      while (!deque.isEmpty() && nums[i] >= nums[deque.peekLast()]) {
        deque.pollLast();
      }
      deque.offerLast(i);
      while (deque.peekFirst() <= i - k) {
        deque.pollFirst();
      }
      ans[i - k + 1] = nums[deque.peekFirst()];
    }
    return ans;
  }

  public static int[] maxSlidingWindow2(int[] nums, int k) {
    int n = nums.length;
    int[] prefixMax = new int[n];
    int[] suffixMax = new int[n];
    for (int i = 0; i < n; i++) {
      if (i % k == 0) {
        prefixMax[i] = nums[i];
      } else {
        prefixMax[i] = Math.max(prefixMax[i - 1], nums[i]);
      }
    }
    for (int i = n - 1; i >= 0; i--) {
      if (i == n - 1 || (i + 1) % k == 0) {
        suffixMax[i] = nums[i];
      } else {
        suffixMax[i] = Math.max(suffixMax[i + 1], nums[i]);
      }
    }
    int[] ans = new int[n - k + 1];
    for (int i = 0; i <= n - k; i++) {
      ans[i] = Math.max(suffixMax[i], prefixMax[i + k - 1]);
    }
    return ans;
  }

```

### minWindow

14. use Map store String define r = -1
15. slide window use while loop in these case use r<len then r++
16. second while loop use check function and l<=r
17. move l use if ori.contains() set valid--

check function aka ori.get(ch).equals(window.get(ch))

!> [!IMPORTANT]
> first while loop if condition must add r < len
> second while loop check then l<=r

```java

  public static boolean check(Map<Character, Integer> ori, Map<Character, Integer> window) {
    Iterator<Map.Entry<Character, Integer>> it = ori.entrySet().iterator();
    while (it.hasNext()) {
      Map.Entry<Character, Integer> entry = (Map.Entry<Character, Integer>) it.next();
      Character key = (Character) entry.getKey();
      Integer val = (Integer) entry.getValue();
      if (window.getOrDefault(key, 0) < val) {
        return false;
      }
    }
    return true;
  }

  public static String minWindow(String s, String t) {
    Map<Character, Integer> ori = new HashMap<>();
    Map<Character, Integer> window = new HashMap<>();

    for (char c : t.toCharArray())
      ori.put(c, ori.getOrDefault(c, 0) + 1);

    int l = 0, r = -1;
    int len = s.length();
    int ans_l = -1, ans_r = -1;
    int minLen = Integer.MAX_VALUE;

    while (r < len) {
      r++;
      if (r < len && ori.containsKey(s.charAt(r))) {
        window.put(s.charAt(r), window.getOrDefault(s.charAt(r), 0) + 1);
      }
      while (check(ori, window) && l <= r) {
        if (r - l + 1 < minLen) {
          minLen = r - l + 1;
          ans_l = l;
          ans_r = l + minLen;
        }
        if (ori.containsKey(s.charAt(l))) {
          window.put(s.charAt(l), window.get(s.charAt(l)) - 1);
        }
        l++;
      }
    }
    return ans_l == -1 ? "" : s.substring(ans_l, ans_r);
  }

```

## plainArray

### maxSubArray

18. dp
19. divide

[reference](https://leetcode.cn/problems/maximum-subarray/solutions/9058/dong-tai-gui-hua-fen-zhi-fa-python-dai-ma-java-dai)

```java

    public static class Status {
        public int lSum, rSum, mSum, iSum;

        public Status(int lSum, int rSum, int mSum, int iSum) {
            this.lSum = lSum;
            this.rSum = rSum;
            this.mSum = mSum;
            this.iSum = iSum;
        }
    }

    public static int maxSubArray2(int[] nums) {
        return getInfo(nums, 0, nums.length - 1).mSum;
    }

    public static Status getInfo(int[] a, int l, int r) {
        if (l == r) {
            return new Status(a[l], a[l], a[l], a[l]);
        }
        int m = (l + r) >> 1;
        Status lSub = getInfo(a, l, m);
        Status rSub = getInfo(a, m + 1, r);
        return pushUp(lSub, rSub);
    }

    public static Status pushUp(Status l, Status r) {
        int iSum = l.iSum + r.iSum;
        int lSum = Math.max(l.lSum, l.iSum + r.lSum);
        int rSum = Math.max(r.rSum, r.iSum + l.rSum);
        int mSum = Math.max(Math.max(l.mSum, r.mSum), l.rSum + r.lSum);
        return new Status(lSum, rSum, mSum, iSum);
    }

    public int maxSubArray1(int[] nums) {
        int pre = 0, maxAns = nums[0];
        for (int x : nums) {
            pre = Math.max(pre + x, x);
            maxAns = Math.max(maxAns, pre);
        }
        return maxAns;
    }

    public static int maxSubArray(int[] nums) {
        int len = nums.length;
        if (len == 0) {
            return 0;
        }
        return maxSubArraySum(nums, 0, len - 1);
    }

    private static int maxCrossingSum(int[] nums, int left, int mid, int right) {
        int sum = 0;
        int leftSum = Integer.MAX_VALUE;
        for (int i = mid; i >= left; i--) {
            sum += nums[i];
            if (sum > leftSum) {
                leftSum = sum;
            }
        }
        sum = 0;
        int rightSum = Integer.MIN_VALUE;
        for (int i = mid + 1; i <= right; i++) {
            sum += nums[i];
            if (sum > rightSum) {
                rightSum = sum;
            }
        }
        return leftSum + rightSum;
    }

    private static int maxSubArraySum(int[] nums, int left, int right) {
        if (left == right) {
            return nums[left];
        }
        int mid = left + (right - left) >> 2;
        return max3(
                maxSubArraySum(nums, left, mid),
                maxSubArraySum(nums, mid + 1, right),
                maxCrossingSum(nums, left, mid, right));
    }

    private static int max3(int num1, int num2, int num3) {
        return Math.max(num1, Math.max(num2, num3));
    }

```

### merge

20. just Math(max)
21. use (a,b)->a`[0]`-b`[0]` replace Comparator

```java

  public static int[][] merge(int[][] intervals) {
    if (intervals.length == 0) {
      return new int[0][2];
    }
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    List<int[]> merged = new ArrayList<>();
    for (int i = 0; i < intervals.length; i++) {
      int l = intervals[i][0], r = intervals[i][1];
      if (merged.size() == 0 || merged.get(merged.size() - 1)[1] < l) {
        merged.add(new int[] { l, r });
      } else {
        merged.get(merged.size() - 1)[1] = Math.max(merged.get(merged.size() - 1)[1], r);
      }
    }
    return merged.toArray(new int[merged.size()][]);
  }

```

### rotate

three methods;
first use additional space
second use gcd since we can find it's a loop
third repeatly use reverse

```java
  public static void rotate(int[] nums, int k) {
    int n = nums.length;
    k %= n;
    int count = gcd(n, k);
    for (int start = 0; start < count; start++) {
      int current = start;
      int prev = nums[start];
      do {
        int next = (current + k) % n;
        int tmp = nums[next];
        nums[next] = prev;
        prev = tmp;
        current = next;
      } while (start != current);
    }
  }

  public static int gcd(int a, int b) {
    return b > 0 ? gcd(b, a % b) : a;
  }
```

### productExceptSelf

two methods;
first use two array store left product and right product then product them aka the answer
second out array first for loop get above left product then reverse use r then answer*=r r*=nums[i];

```java

  public static int[] productExceptSelf(int[] nums) {
    int n = nums.length;
    int[] answer = new int[n];

    answer[0] = 1;
    for (int i = 1; i < n; i++) {
      answer[i] = nums[i - 1] * answer[i - 1];
    }
    int r = 1;
    for (int i = n - 1; i >= 0; i--) {
      answer[i] = answer[i] * r;
      r *= nums[i];
    }
    return answer;
  }

```

### firstMissingPositive

three methods
first use Set then use for loop i find contains(i)
second just use Arrays.sort then binary search
third use hashtable aka treat array as hashtable N map array[N-1]

```java

  public static int firstMissingPositive(int[] nums) {
    int n = nums.length;
    for (int i = 0; i < n; i++) {
      while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
        swap(nums, nums[i] - 1, i);
      }
    }
    for (int i = 0; i < n; i++) {
      if (nums[i] != i + 1) {
        return i + 1;
      }
    }
    return n + 1;
  }

  public static void swap(int[] nums, int index1, int index2) {
    int tmp = nums[index1];
    nums[index1] = nums[index2];
    nums[index2] = tmp;
  }

  public static int firstMissingPositive1(int[] nums) {
    int n = nums.length;
    Arrays.sort(nums);
    for (int i = 1; i <= n; i++) {
      int ans = binarySearch(nums, i);
      if (ans == -1) {
        return i;
      }
    }
    return n + 1;
  }

  public static int binarySearch(int[] nums, int target) {
    int l = 0;
    int r = nums.length - 1;
    while (l <= r) {
      int mid = (l + r) >> 1;
      if (nums[mid] == target) {
        return mid;
      } else if (nums[mid] < target) {
        l = mid + 1;
      } else {
        r = mid - 1;
      }
    }
    return -1;
  }

  public static int firstMissingPositive2(int[] nums) {
    int n = nums.length;
    Set<Integer> hashSet = new HashSet<>();
    for (int num : nums) {
      hashSet.add(num);
    }
    for (int i = 1; i <= n; i++) {
      if (!hashSet.contains(i)) {
        return i;
      }
    }
    return n + 1;
  }

```

## matrix

### setZeroes

just use flag to mark which to assign 0

```java

  public static void setZeroes(int[][] matrix) {
    int m = matrix.length, n = matrix[0].length;
    boolean[] row = new boolean[m];
    boolean[] col = new boolean[n];
    for (int i = 0; i < m; i++) {
      for (int j = 0; j < n; j++) {
        if (matrix[i][j] == 0) {
          row[i] = col[j] = true;
        }
      }
    }
    for (int i = 0; i < m; i++) {
      for (int j = 0; j < n; j++) {
        if (row[i] || col[j]) {
          matrix[i][j] = 0;
        }
      }
    }
  }

  public static void setZeroes1(int[][] matrix) {
    int m = matrix.length, n = matrix[0].length;
    boolean flagCol = false, flagRow = false;
    for (int i = 0; i < m; i++) {
      if (matrix[i][0] == 0) {
        flagCol = true;
      }
    }
    for (int j = 0; j < n; j++) {
      if (matrix[0][j] == 0) {
        flagRow = true;
      }
    }
    for (int i = 1; i < m; i++) {
      for (int j = 1; j < n; j++) {
        if (matrix[i][j] == 0) {
          matrix[i][0] = matrix[0][j] = 0;
        }
      }
    }
    for (int i = 1; i < m; i++) {
      for (int j = 1; j < n; j++) {
        if (matrix[i][j] == 0 || matrix[0][j] == 0) {
          matrix[i][j] = 0;
        }
      }
    }

    if (flagRow) {
      for (int i = 0; i < m; i++) {
        matrix[i][0] = 0;
      }
    }
    if (flagCol) {
      for (int j = 0; j < n; j++) {
        matrix[0][j] = 0;
      }
    }
  }

  public static void setZeroes2(int[][] matrix) {
    int m = matrix.length, n = matrix[0].length;
    boolean flagCol = false;
    for (int i = 0; i < m; i++) {
      if (matrix[i][0] == 0) {
        flagCol = true;
      }
      for (int j = 1; j < n; j++) {
        if (matrix[i][j] == 0) {
          matrix[i][0] = matrix[0][j] = 0;
        }
      }
    }
    for (int i = m - 1; i >= 0; i--) {
      for (int j = 1; j < n; j++) {
        if (matrix[i][0] == 0 || matrix[0][j] == 0) {
          matrix[i][j] = 0;
        }
      }
      if (flagCol) {
        matrix[i][0] = 0;
      }
    }
  }

```

### spiralOrder

two method
first use visited array auxiliary then use four directions
like map
second use four pointer mean is if(++u>d) break set boundary

```java

  public static List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> ans = new ArrayList<>();
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
      return ans;
    }
    int u = 0, d = matrix.length - 1;
    int l = 0, r = matrix[0].length - 1;
    while (true) {
      for (int i = l; i <= r; i++) {
        ans.add(matrix[u][i]);
      }
      if (++u > d) {
        break;
      }
      for (int i = u; i <= d; i++) {
        ans.add(matrix[i][r]);
      }
      if (--r < l) {
        break;
      }
      for (int i = r; i >= l; i--) {
        ans.add(matrix[d][i]);
      }
      if (--d < u) {
        break;
      }
      for (int i = d; i >= u; i--) {
        ans.add(matrix[i][l]);
      }
      if (++l > r) {
        break;
      }
    }
    return ans;
  }

  public static List<Integer> spiralOrder1(int[][] matrix) {
    List<Integer> order = new ArrayList<>();
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
      return order;
    }
    int rows = matrix.length, cols = matrix[0].length;
    boolean[][] visited = new boolean[rows][cols];
    int total = rows * cols;
    int row = 0, col = 0;
    int[][] directions = { { 0, 1 }, { 1, 0 }, { 0, -1 }, { -1, 0 } };
    int directionIndex = 0;
    for (int i = 0; i < total; i++) {
      order.add(matrix[row][col]);
      visited[row][col] = true;
      int newRow = row + directions[directionIndex][0], newCol = col + directions[directionIndex][1];
      if (newRow < 0 || newRow >= rows || newCol < 0 || newCol >= cols || visited[row][col]) {
        directionIndex = (directionIndex + 1) % 4;
      }
      row += directions[directionIndex][0];
      col += directions[directionIndex][1];
    }
    return order;
  }

```

### rotate

familiar with matrix rotation like vertical horizontal diagonal

```java

  public static void rotate(int[][] matrix) {
    int n = matrix.length;
    for (int i = 0; i < n / 2; i++) {
      for (int j = 0; j < n; j++) {
        int tmp = matrix[i][j];
        matrix[i][j] = matrix[n - i - 1][j];
        matrix[n - i - 1][j] = tmp;
      }
    }
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < i; j++) {
        int tmp = matrix[i][j];
        matrix[i][j] = matrix[j][i];
        matrix[j][i] = tmp;
      }
    }
  }

```

### searchMatrix

z search

if > then y-- else x++

```java

  public static boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length, n = matrix[0].length;
    int x = 0, y = n - 1;
    while (x < m && y >= 0) {
      if (matrix[x][y] == target) {
        return true;
      }
      if (matrix[x][y] > target) {
        y--;
      } else {
        x++;
      }
    }
    return false;
  }

```

## linkedList

### getIntersectionNode

two method
first use hashset
second returnlen1+len2+common

```java

  public static ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    if (headA == null || headB == null) {
      return null;
    }
    ListNode pA = headA, pB = headB;
    while (pA != pB) {
      pA = pA == null ? headA : pA.next;
      pB = pB == null ? headB : pB.next;
    }
    return pA;
  }

  public static ListNode getIntersectionNode1(ListNode headA, ListNode headB) {
    Set<ListNode> visited = new HashSet<>();
    ListNode tmp = headA;
    while (tmp != null) {
      visited.add(tmp);
      tmp = tmp.next;
    }
    tmp = headB;
    while (tmp != null) {
      if (visited.contains(tmp)) {
        return tmp;
      }
    }
    return null;
  }

```

### reverseList

first use prev and cur then just while loop cur!=null
second use recursion considering n<sub>k</sub> state n<sub>k+1</sub>.next.next = n<sub>k</sub> n <sub>k+1</sub>.next = null

```java

  public static ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) {
      return head;
    }
    ListNode newHead = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return newHead;
  }

  public static ListNode reverseList1(ListNode head) {
    ListNode prev = null;
    ListNode cur = head;
    while (cur != null) {
      ListNode next = cur.next;
      cur.next = prev;
      prev = cur;
      cur = next;
    }
    return prev;
  }

```

### isPalindrome

first use two pointer and ArrayList front ++ back--
second use recursive just compare front and last
third use stack
forth use fast and slow point
since we can get half and tail so we just reverse tail then compare
last recovery

```java

  public static ListNode reverseList(ListNode head) {
    ListNode pre = null;
    ListNode cur = head;
    while (cur != null) {
      ListNode tmp = cur.next;
      cur.next = pre;
      pre = cur;
      cur = tmp;
    }
    return pre;
  }

  public static ListNode endOfFirstHalf(ListNode head) {
    ListNode fast = head;
    ListNode slow = head;
    while (fast.next != null && fast.next.next != null) {
      fast = fast.next.next;
      slow = slow.next;
    }
    return slow;
  }

  public static boolean isPalindrome0(ListNode head) {
    if (head == null) {
      return true;
    }
    ListNode firstHalfEnd = endOfFirstHalf(head);
    ListNode secondHalfStart = reverseList(firstHalfEnd.next);
    ListNode p1 = head;
    ListNode p2 = secondHalfStart;
    boolean result = true;
    while (result && p2 != null) {
      if (p1.val != p2.val) {
        result = false;
      }
      p1 = p1.next;
      p2 = p2.next;
    }
    firstHalfEnd.next = reverseList(secondHalfStart);
    return result;
  }

  public static boolean isPalindrome(ListNode head) {
    Stack<Integer> stack = new Stack<>();
    ListNode cur = head;
    while (cur != null) {
      stack.push(cur.val);
      cur = cur.next;
    }
    cur = head;
    while (cur != null) {
      if (cur.val != stack.peek()) {
        return false;
      }
      stack.pop();
      cur = cur.next;
    }
    return true;
  }

  private static ListNode front;

  private static boolean recursivelyCheck(ListNode cur) {
    if (cur != null) {
      if (!recursivelyCheck(cur.next)) {
        return false;
      }
      if (cur.val != front.val) {
        return false;
      }
      front = front.next;
    }
    return true;
  }

  public static boolean isPalindrome1(ListNode head) {
    front = head;
    return recursivelyCheck(head);
  }

  public static boolean isPalindrome2(ListNode head) {
    List<Integer> vals = new ArrayList<>();
    ListNode cur = head;
    while (cur != null) {
      vals.add(cur.val);
      cur = cur.next;
    }
    int front = 0;
    int back = vals.size() - 1;
    while (front < back) {
      if (!vals.get(front).equals(vals.get(back))) {
        return false;
      }
      front++;
      back--;
    }
    return true;
  }

```

### hasCycle

first use set since set.add() return boolean
second use fast slow pointer while condition is fast!=slow

```java

  public static boolean hasCycle(ListNode head) {
    if (head == null || head.next == null) {
      return false;
    }
    ListNode slow = head;
    ListNode fast = head.next;
    while (slow != fast) {
      if (fast == null || fast.next == null) {
        return false;
      }
      slow = slow.next;
      fast = fast.next.next;
    }
    return true;
  }

  public static boolean hasCycle1(ListNode head) {
    Set<ListNode> set = new HashSet<>();
    while (head != null) {
      if (!set.add(head)) {
        return true;
      }
      head = head.next;
    }
    return false;
  }

```

### detectCycle

math inference can show after slow meet fast
ptr meet slow is the cycle entrence

```java

  public static ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (true) {
      if (fast == null || fast.next == null) {
        return null;
      }
      fast = fast.next.next;
      slow = slow.next;
      if (fast == slow) {
        break;
      }
    }
    ListNode ptr = head;
    while (ptr != slow) {
      ptr = ptr.next;
      slow = slow.next;
    }
    return ptr;
  }

```

### mergeTwoLists

recursive just continue add big val
iterator just intrinsic

```java

  public static ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode prehead = new ListNode(-1);
    ListNode pre = prehead;
    while (l1 != null && l2 != null) {
      if (l1.val <= l2.val) {
        pre.next = l1;
        l1 = l1.next;
      } else {
        pre.next = l2;
        l2 = l2.next;
      }
      pre = pre.next;
    }

    pre.next = l1 == null ? l2 : l1;
    return prehead.next;
  }

  public static ListNode mergeTwoLists1(ListNode l1, ListNode l2) {
    if (l1 == null) {
      return l2;
    } else if (l2 == null) {
      return l1;
    } else if (l1.val < l2.val) {
      l1.next = mergeTwoLists(l1.next, l2);
      return l1;
    } else {
      l2.next = mergeTwoLists(l1, l2.next);
      return l2;
    }
  }

  public static void printList(ListNode head) {
    ListNode current = head;
    while (current != null) {
      System.out.print(current.val + " ");
      current = current.next;
    }
    System.out.println();
  }
```

### addTwoNumbers

common but you should mention
while loop condition use ||
use head and tail parameters
then initial use head == null
head = tail = new ListNode(sum%10)

```java

  public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode head = null, tail = null;
    int carry = 0;
    while (l1 != null || l2 != null) {
      int n1 = l1 != null ? l1.val : 0;
      int n2 = l2 != null ? l2.val : 0;
      int sum = n1 + n2 + carry;
      if (head == null) {
        head = tail = new ListNode(sum % 10);
      } else {
        tail.next = new ListNode(sum % 10);
        tail = tail.next;
      }
      carry = sum / 10;
      if (l1 != null) {
        l1 = l1.next;
      }
      if (l2 != null) {
        l2 = l2.next;
      }
    }
    if (carry > 0) {
      tail.next = new ListNode(carry);
    }
    return head;
  }

```

### removeNthFromEnd

think it then no need to consider head and tail
first just get length then for loop len-n+1
second use stack then pop n
third first = second + n

```java

  public static ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0, head);
    ListNode first = head;
    ListNode second = dummy;
    for (int i = 0; i < n; i++) {
      first = first.next;
    }
    while (first != null) {
      first = first.next;
      second = second.next;
    }
    second.next = second.next.next;
    ListNode ans = dummy.next;
    return ans;
  }

  public static ListNode removeNthFromEnd1(ListNode head, int n) {
    ListNode dummy = new ListNode(0, head);
    Deque<ListNode> stack = new LinkedList<>();
    ListNode cur = dummy;
    while (cur != null) {
      stack.push(cur);
      cur = cur.next;
    }
    for (int i = 0; i < n; i++) {
      stack.pop();
    }
    ListNode pre = stack.peek();
    pre.next = pre.next.next;
    ListNode ans = dummy.next;
    return ans;
  }

  public static ListNode removeNthFromEnd2(ListNode head, int n) {
    ListNode dummy = new ListNode(0, head);
    int len = getLength(head);
    ListNode cur = dummy;
    for (int i = 1; i < len - n + 1; i++) {
      cur = cur.next;
    }
    cur.next = cur.next.next;
    ListNode ans = dummy.next;
    return ans;
  }

  public static int getLength(ListNode head) {
    int len = 0;
    while (head != null) {
      len++;
      head = head.next;
    }
    return len;
  }

```

### swapPairs

my error is let second no pre cause error

```java
  public static ListNode swapPairs(ListNode head) {
    ListNode dummy = new ListNode(0, head);
    ListNode first = dummy.next , second = null;
    while (first != null && first.next != null) {
      second = first.next;
      first.next = second.next;
      second.next = first;
      first = first.next;
    }
    return dummy.next;
```

fixed

```java
public static ListNode swapPairs(ListNode head) {
    ListNode dummy = new ListNode(0, head);
    ListNode first = dummy.next , second = null;
    ListNode pre = dummy;
    while (first != null && first.next != null) {
      second = first.next;
      first.next = second.next;
      pre.next = second;
      second.next = first;
      pre = first;
      first = first.next;
    }
    return dummy.next;
}
```

```java

  public static ListNode swapPairs(ListNode head) {
    ListNode dummy = new ListNode(0, head);
    ListNode pre = dummy;
    while (pre.next != null && pre.next.next != null) {
      ListNode first = pre.next;
      ListNode second = first.next;

      pre.next = second;
      first.next = second.next;
      second.next = first;
      pre = first;
    }
    return dummy.next;
  }
```
