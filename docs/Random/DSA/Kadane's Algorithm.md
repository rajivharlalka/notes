- for finding the max sum of contiguous subarray of a given length.
- Time Complexity - O(n)
- All numbers should be non-negative.
- For negative numbers [[Maximum subarray problem algorithm]] should be used.
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
      int n = nums.size(); 
      // globalSum is where the maximum sum of subarray is stored
      // localSum is where the sum of current subarray is stored
      int globalSum = INT_MIN, localSum = 0;
      for (int i = 0; i < n; i++) {
        // add current element to current sum 
        localSum = localSum + nums[i];
        // if current sum is greater than globalSum, update globalSum
        if (globalSum < localSum) {
          globalSum = localSum;
        }
        // if upon adding ith element current sum is becoming less than 0
        // it cannot contribute to the maximum sum subarray so we neglect it 
        // and reset our current sum to 0 to start another subarray freshly
        if (localSum < 0) {
          localSum = 0;
        }
      }
      return globalSum;
    }
};
```