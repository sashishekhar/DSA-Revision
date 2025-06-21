# 1. Largest Element in an Array.
### Multiple ways, we can use inbuilt function max or we can run linear search updating the max variable.

# 2. Second largest Element.
### App1
```txt
we can have two seperate for-loops, first one will
find the largest element in the array and the second
element will also find the largest element but it will
compare with the largest element and it should be smaller than that.
```
### App2
```txt
anathor way it can be done,
we can use a single for-loop,
in this we will have two variable, its easy, work out in the code
// do clearout if there are duplicates, it can change the approch
```

# 3. Check if array sorted.
### Esy just maintain two variables, iterate, check i<=j, solved

# 4. Remove duplicates from the sorted array
### Alaways clearout from the interviewr first, whats he is asking, there can be many variations like if he is asking to use the same given array or we can take a ans array, and do solve accordingly.,, two pointers can be used in  case.

### Two Scenarios
### a. if sorted array
```
if the array is sorted, we will require an answer array,
and we will be keep pushing unique elements in the ans array, return ans array.
```

### b. unsorted array
```
if unsorted, we can simply maintain a hashset, and then return the hashset
into and answer array
```

# 5. Rotate array.
## a. left, by one place
```
store first element
mke arr[i]= arr[i+1], last element = first element
```
## b. by d places
### app1- simple iterate - extra space
```
its simple like we rotated by one place
```
```
void Rotatetoleft(int arr[], int n, int k)
{
  if (n == 0)
    return;
  k = k % n;
  if (k > n)
    return;
  int temp[k];
  for (int i = 0; i < k; i++)
  {
    temp[i] = arr[i];
  }
  for (int i = 0; i < n - k; i++)
  {
    arr[i] = arr[i + k];
  }
  for (int i = n - k; i < n; i++)
  {
    arr[i] = temp[i - n + k];
  }
}
```
### app2- make a reverse function - optimized
```
void Reverse(int arr[], int start, int end)
{
  while (start <= end)
  {
    int temp = arr[start];
    arr[start] = arr[end];
    arr[end] = temp;
    start++;
    end--;
  }
}
// Function to Rotate k elements to right
void Rotateeletoright(int arr[], int n, int k)
{
  // Reverse first n-k elements
  Reverse(arr, 0, n - k - 1);
  // Reverse last k elements
  Reverse(arr, n - k, n - 1);
  // Reverse whole array
  Reverse(arr, 0, n - 1);
}
```

# 6. Union of two arrays.
### App1
```
Hashmap
```
### App2
```
*Set*
set < int > s;
  vector < int > Union;
  for (int i = 0; i < n; i++)
    s.insert(arr1[i]);
  for (int i = 0; i < m; i++)
    s.insert(arr2[i]);
  for (auto & it: s)
    Union.push_back(it);
  return Union;
```

### App3 - Most optimized
```
first sort both array
Two Pointer, its easy
```
# 7. Longest subarray with given sum k
## only positive no.
```
3 loops
```
```
2 loops
```
```
use hashing + prefix sum
```
```
//using two pointers

int getLongestSubarray(vector<int>& a, long long k) {
    int n = a.size(); // size of the array.

    int left = 0, right = 0; // 2 pointers
    long long sum = a[0];
    int maxLen = 0;
    while (right < n) {
        // if sum > k, reduce the subarray from left
        // until sum becomes less or equal to k:
        while (left <= right && sum > k) {
            sum -= a[left];
            left++;
        }

        // if sum = k, update the maxLen i.e. answer:
        if (sum == k) {
            maxLen = max(maxLen, right - left + 1);
        }

        // Move forward thw right pointer:
        right++;
        if (right < n) sum += a[right];
    }

    return maxLen;
}

```
## positive + negative no.
```
3 loops
```
```
2 loops
```
```
use hashing + prefix sum
int longestsubarray(vector<int> a, long long k){
  int acc = *accumulate(a.begin(),a.end(),0);
  int sum=0;maxlen =0;int len=0;
  if(acc == k) return a.size();
  map<int,int> presummap;
  for(int i=0;i<a.size;i++){
    sum += a[i];
    if(sum == k){
      len = i+1;
      maxlen = max(maxlen,len);
    }
    int rem = k-sum;
    if(presummap.find(rem) != presummap.end()){
      len = i-presummap[rem];
      maxlen = max(maxlen,len);
    }
    if (preSumMap.find(sum) == preSumMap.end()) {
            preSumMap[sum] = i;
        }
  }
  return maxlen;
}
```





