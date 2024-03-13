# Sliding window

This template can be customized based on specific problem requirements, such as finding the maximum sum subarray, counting distinct elements, or finding a target subarray sum.

## Template:

```cpp
void slidingWindow(const vector<int>& arr, int k) {
    int n = arr.size();
    
    // Initialize variables for the window
    int windowStart = 0;
    int windowSum = 0;
    
    // Iterate through the array
    for (int windowEnd = 0; windowEnd < n; windowEnd++) {
        // Expand the window
        windowSum += arr[windowEnd];
        
        // Check if the window size is greater than k
        if (windowEnd >= k - 1) {
            // Process the window
            
            // Compute the result or do some operation
            
            // Shrink the window
            windowSum -= arr[windowStart];
            windowStart++;
        }
    }
}
```

## use case:

1.  **Maximum Sum Subarray of Size K:** Given an array of integers and a positive integer K, find the maximum sum of a contiguous subarray of size K.

    ```cpp
    int maxSumSubarray(const vector<int>& arr, int k) {
        int n = arr.size();
        int maxSum = 0;
        int windowSum = 0;

        for (int i = 0; i < k; i++) {
            windowSum += arr[i];
        }
        maxSum = windowSum;

        for (int i = k; i < n; i++) {
            windowSum += arr[i] - arr[i - k];
            maxSum = max(maxSum, windowSum);
        }

        return maxSum;
    }
    ```
2.  **Longest Subarray with at Most K Distinct Characters:** Given a string, find the length of the longest substring with at most K distinct characters.

    ```cpp
    int longestSubstringWithKDistinct(const string& str, int k) {
        int n = str.size();
        unordered_map<char, int> freq;
        int maxLength = 0;
        int windowStart = 0;

        for (int windowEnd = 0; windowEnd < n; windowEnd++) {
            freq[str[windowEnd]]++;

            while (freq.size() > k) {
                freq[str[windowStart]]--;
                if (freq[str[windowStart]] == 0)
                    freq.erase(str[windowStart]);
                windowStart++;
            }

            maxLength = max(maxLength, windowEnd - windowStart + 1);
        }

        return maxLength;
    }
    ```
3.  **Subarray Product Less Than K:** Given an array of positive integers and an integer K, find the number of contiguous subarrays where the product of all elements is less than K.

    ```cpp
    int numSubarrayProductLessThanK(const vector<int>& nums, int k) {
        int n = nums.size();
        int count = 0;
        int windowStart = 0;
        int product = 1;

        for (int windowEnd = 0; windowEnd < n; windowEnd++) {
            product *= nums[windowEnd];

            while (windowStart <= windowEnd && product >= k) {
                product /= nums[windowStart];
                windowStart++;
            }

            count += windowEnd - windowStart + 1;
        }

        return count;
    }
    ```

These are just a few examples, but the sliding window technique is versatile and can be applied to a wide range of problems where you need to efficiently process subarrays or substrings within a larger data structure.
