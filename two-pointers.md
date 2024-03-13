# Two pointers

## Template:

```cpp
#include <vector>
using namespace std;

int processArray(vector<int>& array) {
    // Initializing two pointers at opposite ends of the array
    int leftPointer = 0;
    int rightPointer = int(array.size()) - 1;

    // Variable to store the result of some operation
    int result = 0;

    // Loop until the left pointer crosses or meets the right pointer
    while (leftPointer < rightPointer) {
        // Perform some logic here using the values at leftPointer and rightPointer
        // If certain condition is met, move the left pointer towards right
        // Otherwise, move the right pointer towards left
        if (CONDITION) {
            leftPointer++;
        } else {
            rightPointer--;
        }
    }

    // Return the final result after processing the array
    return result;
}

```

## **use case:**

1. **Finding the Sum of Two Numbers**: Suppose you're given a sorted array of integers, and you need to find two numbers that sum up to a target value. You can use the two-pointer technique to efficiently find these numbers.

```cpp
int findSumPair(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;

    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            return 1; // Found a pair with the sum equal to the target
        } else if (sum < target) {
            left++; // Move left pointer to increase the sum
        } else {
            right--; // Move right pointer to decrease the sum
        }
    }

    return 0; // No pair found with the sum equal to the target
}
```

2. **Finding the Maximum Area of Container**: Given an array of non-negative integers representing the heights of bars, you need to find the container with the maximum area formed by two lines. This problem can also be solved using the two-pointer technique.

```cpp
int maxArea(vector<int>& height) {
    int maxArea = 0;
    int left = 0;
    int right = height.size() - 1;

    while (left < right) {
        int minHeight = min(height[left], height[right]);
        int currArea = (right - left) * minHeight;
        maxArea = max(maxArea, currArea);

        if (height[left] < height[right]) {
            left++; // Move left pointer to potentially increase the area
        } else {
            right--; // Move right pointer to potentially increase the area
        }
    }

    return maxArea;
}
```

These are just two examples of how you can apply the two-pointer technique to solve different problems efficiently.
