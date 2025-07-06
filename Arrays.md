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
# 7. Longest subarray with given sum k ⭐
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
#include <bits/stdc++.h>
using namespace std;

int longestsubarray(vector<int> a, long long k) {
    long long sum = 0;
    int maxlen = 0;
    unordered_map<long long, int> preSumMap;

    for (int i = 0; i < a.size(); i++) {
        sum += a[i];

        // Dry run for a = [1, 2, -1, 4, -2, 1], k = 4
        // i = 0, a[i] = 1 → sum = 1
        // sum != k, sum - k = -3 → not in map
        // Add 1:0 to map

        // i = 1, a[i] = 2 → sum = 3
        // sum != k, sum - k = -1 → not in map
        // Add 3:1 to map

        // i = 2, a[i] = -1 → sum = 2
        // sum != k, sum - k = -2 → not in map
        // Add 2:2 to map

        // i = 3, a[i] = 4 → sum = 6
        // sum != k, sum - k = 2 → ✅ found 2 at index 2
        // len = 3 - 2 = 1 → maxlen = 1
        // Add 6:3 to map

        // i = 4, a[i] = -2 → sum = 4
        // sum == k → maxlen = max(1, 4 + 1) = 5
        // Add 4:4 to map

        // i = 5, a[i] = 1 → sum = 5
        // sum != k, sum - k = 1 → ✅ found 1 at index 0
        // len = 5 - 0 = 5 → maxlen remains 5
        // Add 5:5 to map

        if (sum == k) {
            maxlen = i + 1;
        }

        long long rem = sum - k;
        if (preSumMap.find(rem) != preSumMap.end()) {
            int len = i - preSumMap[rem];
            maxlen = max(maxlen, len);
        }

        if (preSumMap.find(sum) == preSumMap.end()) {
            preSumMap[sum] = i;
        }
    }

    return maxlen;
}

int main() {
    vector<int> a = {1, 2, -1, 4, -2, 1};
    int k = 4;
    cout << "Longest subarray with sum = " << k << " is of length: "
         << longestsubarray(a, k) << endl;
    return 0;
}

```
# 8. Two Sum
#### App 1: two loops -> arr[i] + arr[j] == target  {N SQUARE}
#### App 2: hashmap -> find the complement {N and N(SC)}
#### App 3: sort and two pointer {NlogN}

# 9. Sort 0s,1s,2s
#### App 1: simply sort 🫡 ____ NlogN
#### App 2: three count variable, mutate array _____ N+N
#### App 3: Dutch National Flag Algo
![image](https://github.com/user-attachments/assets/4d8c6a39-a275-4c8c-9457-fe37090d7b4c)

# 10. Majority Element
#### App 1: Hashmap
#### App 2: Moore Voting Algo
![image](https://github.com/user-attachments/assets/a71298e9-06fa-4cf1-a411-d18f10ac84cf)

# 11. Max Subarray Sum
#### App 1: 3 loops -> i , j , sum
#### App 2: 2 loops 
#### App 3: Kadane algo
```
long long maxSubarraySum(int arr[], int n) {
    long long maxi = LONG_MIN; // maximum sum
    long long sum = 0;

    for (int i = 0; i < n; i++) {

        sum += arr[i];

        if (sum > maxi) {
            maxi = sum;
        }

        // If sum < 0: discard the sum calculated
        if (sum < 0) {
            sum = 0;
        }
    }

    // To consider the sum of the empty subarray
    // uncomment the following check:

    //if (maxi < 0) maxi = 0;

    return maxi;
}
```
#### Follow up question( print the subarray )
If we carefully observe our algorithm, we can notice that the subarray always starts at the particular index where the sum variable is equal to 0, and at the ending index, the sum always crosses the previous maximum sum(i.e. maxi).

So, we will keep a track of the starting index inside the loop using a start variable.
We will take two variables ansStart and ansEnd initialized with -1. And when the sum crosses the maximum sum, we will set ansStart to the start variable and ansEnd to the current index i.e. i.
The rest of the approach will be the same as Kadane’s Algorithm.

```
long long maxSubarraySum(int arr[], int n) {
    long long maxi = LONG_MIN; // maximum sum
    long long sum = 0;

    int start = 0;
    int ansStart = -1, ansEnd = -1;
    for (int i = 0; i < n; i++) {

        if (sum == 0) start = i; // starting index

        sum += arr[i];

        if (sum > maxi) {
            maxi = sum;

            ansStart = start;
            ansEnd = i;
        }

        // If sum < 0: discard the sum calculated
        if (sum < 0) {
            sum = 0;
        }
    }

    //printing the subarray:
    cout << "The subarray is: [";
    for (int i = ansStart; i <= ansEnd; i++) {
        cout << arr[i] << " ";
    }
    cout << "]n";

    // To consider the sum of the empty subarray
    // uncomment the following check:

    //if (maxi < 0) maxi = 0;

    return maxi;
}
```

# 12. Stock Buy and Sell
#### App 1: two loops -> first loop 0-n and 2nd loop i - n,  maintain an maxpro 
#### App 2: 
Create a variable maxPro and store 0 initially.
Create a variable minPrice and store some larger value(ex: MAX_VALUE) value initially.
Run a for loop from 0 to n.
Update the minPrice if it is greater than the current element of the array
Take the difference of the minPrice with the current element of the array and compare and maintain it in maxPro.
Return the maxPro.

# 13. Make this Array [-1,3,4,5,-1,-4] to [3,-1,4,-1,5,-4],, +,-,+,-...
#### App 1: maintain two array posarr and negarr
#### App 2: maintain two pointers posidx and negidx, run a loop(i), if arr[i]  <0 , arr[negidx] = arr[i], negidx+=2 and vice versa.

# 14. Next prmutation
#### App 1: next_permutation function 
#### App 2: find breakpoint(arr[i] < arr[i+1]) from back of the arr, swap, and u got the next permutation

# 15. Longest Consecutive sequence in array [1,4,2,7,3,9] --> [1,2,3,4]
#### App 1: simple NlogN soln by sorting;
#### App 2: more optimal O(n) --> make a unordered set, then iterate
```
int longestSuccessiveElements(vector<int>&a) {
    int n = a.size();
    if (n == 0) return 0;

    int longest = 1;
    unordered_set<int> st;
    //put all the array elements into set:
    for (int i = 0; i < n; i++) {
        st.insert(a[i]);
    }

    //Find the longest sequence:
    for (auto it : st) {
        //if 'it' is a starting number:
        if (st.find(it - 1) == st.end()) {
            //find consecutive numbers:
            int cnt = 1;
            int x = it;
            while (st.find(x + 1) != st.end()) {
                x = x + 1;
                cnt = cnt + 1;
            }
            longest = max(longest, cnt);
        }
    }
    return longest;

}

```

# 16. Set Matrix Zeroes-- if a cell is zero, make the full row and column zero
#### App 1: lot of naive approches 
#### App 2: use multiple flags, use first row and first column as flag for the whole matrix
its simple 
```
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    bool firstRowZero = false, firstColZero = false;

    // Check if first row has any 0s
    for (int j = 0; j < n; j++) {
        if (matrix[0][j] == 0) {
            firstRowZero = true;
            break;
        }
    }

    // Check if first column has any 0s
    for (int i = 0; i < m; i++) {
        if (matrix[i][0] == 0) {
            firstColZero = true;
            break;
        }
    }

    // Use first row and column as flags
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }

    // Zero rows based on flags
    for (int i = 1; i < m; i++) {
        if (matrix[i][0] == 0) {
            for (int j = 1; j < n; j++) {
                matrix[i][j] = 0;
            }
        }
    }

    // Zero columns based on flags
    for (int j = 1; j < n; j++) {
        if (matrix[0][j] == 0) {
            for (int i = 1; i < m; i++) {
                matrix[i][j] = 0;
            }
        }
    }

    // Finally, zero first row and column if needed
    if (firstRowZero) {
        for (int j = 0; j < n; j++) matrix[0][j] = 0;
    }

    if (firstColZero) {
        for (int i = 0; i < m; i++) matrix[i][0] = 0;
    }
}

};
```

# 17. Rotate Matrix by 90 degree
#### App 1: Naive, have an ans matrix make each row starting from top the column of ans matrix from the last,
#### App 2: when u compare both the matrix, u will notice that we will  get the ans matrix just by transposing the parent matrix and then reversing eachrow;
```
using namespace std;
void rotate(vector < vector < int >> & matrix) {
    int n = matrix.size();
    //transposing the matrix
    for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        swap(matrix[i][j], matrix[j][i]);
    }
    }
    //reversing each row of the matrix
    for (int i = 0; i < n; i++) {
    reverse(matrix[i].begin(), matrix[i].end());
    }
}
```

# 18. Spriral traversal of matrix
```
have 4 pointers top(toprow), right(rightcol), bottom(bottomrow), left(leftcol); run 4 seperate loop to print all 4 sides, after printing each side increment or decrement pointers , and encapsulate all this 4 loops into a single while, for printing all the square layers of the matrix,

vector<int> printSpiral(vector<vector<int>> mat) {
 
  // Define ans array to store the result.
  vector<int> ans;
 
  int n = mat.size(); // no. of nows
  int m = mat[0].size(); // no. of columns
  
  // Initialize the pointers reqd for traversal.
  int top = 0, left = 0, bottom = n - 1, right = m - 1;

  // Loop until all elements are not traversed.
  while (top <= bottom && left <= right) {
      
    // For moving left to right
    for (int i = left; i <= right; i++)
      ans.push_back(mat[top][i]);

    top++;

    // For moving top to bottom.
    for (int i = top; i <= bottom; i++)
      ans.push_back(mat[i][right]);

    right--;
    
    // For moving right to left.
    if (top <= bottom) {
      for (int i = right; i >= left; i--)
       ans.push_back(mat[bottom][i]);

      bottom--;
    }

    // For moving bottom to top.
    if (left <= right) {
      for (int i = bottom; i >= top; i--)
        ans.push_back(mat[i][left]);

      left++;
    }
  }
  return ans;
}
```

# 19. Count subarrays with sum k
#### App 1 ,2 : 3 loops and 2 loops
#### optimal app
```
Assume, the prefix sum of a subarray ending at index i is x. In that subarray, we will search for another subarray ending at index i, whose sum equals k. Here, we need to observe that if there exists another subarray ending at index i with sum k, then the prefix sum of the rest of the subarray will be x-k. The below image will clarify the concept:


Now, for a subarray ending at index i with the prefix sum x, if we remove the part with the prefix sum x-k, we will be left with the part whose sum is equal to k. And that is what we want.

Now, there may exist multiple subarrays with the prefix sum x-k. So, the number of subarrays with sum k that we can generate from the entire subarray ending at index i, is exactly equal to the number of subarrays with the prefix sum x-k, that we can remove from the entire subarray.

That is why, instead of searching the subarrays with sum k, we will keep the occurrence of the prefix sum of the subarrays using a map data structure. 

In the map, we will store every prefix sum calculated, with its occurrence in a <key, value> pair. Now, at index i, we just need to check the map data structure to get the number of times that the subarrays with the prefix sum x-k occur. Then we will simply add that number to our answer.

We will apply the above process for all possible indices of the given array. The possible values of the index i can be from 0 to n-1(where n = size of the array).


class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int n = nums.size(); // size of the given array.
        map<int,int> mpp;
        int preSum = 0, cnt = 0;

        mpp[0] = 1; // Setting 0 in the map.
        for (int i = 0; i < n; i++) {
        // add current element to prefix Sum:
            preSum += nums[i];

        // Calculate x-k:
            int remove = preSum - k;

        // Add the number of subarrays to be removed:
            cnt += mpp[remove];

        // Update the count of prefix sum
        // in the map.
            mpp[preSum] += 1;
        }
    return cnt;
        
    }
};
```




