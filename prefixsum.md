# PrefixSum

This function takes an input vector `arr` and returns another vector containing the prefix sums of the elements in `arr`. It iterates through the input array, calculating the cumulative sum up to each element and storing the results in the output vector.

## Template:

```cpp
#include <vector>
using namespace std;

// Function to calculate prefix sums of an array
vector<int> calculatePrefixSums(vector<int>& arr) {
    // Create a vector to store prefix sums with the same size as the input array
    vector<int> prefixSums(arr.size());

    // First element of the prefix sums is the same as the first element of the array
    prefixSums[0] = arr[0];

    // Iterate through the array to compute prefix sums
    for (int i = 1; i < arr.size(); i++) {
        // Each prefix sum is the sum of all elements from index 0 up to the current index
        prefixSums[i] = prefixSums[i - 1] + arr[i];
    }

    // Return the vector containing prefix sums
    return prefixSums;
}

```

## use case:

1.  **Range Sum Queries**: Suppose you have an array representing some values, and you need to efficiently answer queries of the form "what is the sum of elements in a certain range?". By precomputing the prefix sums, you can quickly compute the sum of any range by subtracting the prefix sum at the start of the range from the prefix sum just after the end of the range.

    ```cpp
    vector<int> arr = {1, 2, 3, 4, 5};
    vector<int> prefixSums = calculatePrefixSums(arr);
    // Range sum from index 1 to 3 (inclusive)
    int sum = prefixSums[3] - prefixSums[0] + arr[0];
    ```
2.  **Efficient Update Operations**: If you need to perform a lot of update operations on an array (e.g., incrementing elements at certain indices), maintaining prefix sums can make updates more efficient. You can update the prefix sums array after each modification, enabling constant-time range sum queries.

    ```cpp
    vector<int> arr = {0, 0, 0, 0, 0}; // Initialize array with zeros
    vector<int> prefixSums = calculatePrefixSums(arr);
    // Increment elements from index 1 to 3 by 2
    for (int i = 1; i <= 3; i++) {
        arr[i] += 2;
    }
    // Update prefix sums after modification
    prefixSums = calculatePrefixSums(arr);
    ```
3.  **Finding Subarray Sums**: You might need to find all subarray sums efficiently. With prefix sums, you can find the sum of any subarray by simply subtracting two prefix sums.

    ```cpp
    vector<int> arr = {1, 2, 3, 4, 5};
    vector<int> prefixSums = calculatePrefixSums(arr);
    // Sum of subarray from index 2 to 4
    int subarraySum = prefixSums[4] - prefixSums[1]; 
    ```

These are just a few examples. The prefix sum technique is widely used in various algorithms and data structures to optimize computations involving cumulative sums.
