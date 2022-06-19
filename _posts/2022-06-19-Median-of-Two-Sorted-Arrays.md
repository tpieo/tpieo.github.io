---
title: Median of Two Sorted Arrays
categories: ["Leetcode"]
---
[https://leetcode.cn/problems/median-of-two-sorted-arrays/](https://leetcode.cn/problems/median-of-two-sorted-arrays/)
```
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).
```

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {

        // make nums1 is the shorter array
        if (nums1.size() > nums2.size()) {
            std::swap(nums1, nums2);
        }
        
        int m = (int)nums1.size(), n = (int)nums2.size();

        // make left get more element if total is odd
        int totalLeft = (m + n + 1) / 2;

        int left = 0, right = m;

        while (left < right) {
            // make i in the right of the dividing line
            // that make i also represent amount of left elements
            int i = left + (right - left + 1) / 2;
            int j = totalLeft - i;
            if (nums1[i-1] > nums2[j]) {
                right = i - 1; // [left, i-1]
            } else {
                left = i; // [i, right]
            }
        }

        int i = left;
        int j = totalLeft - i;
        int nums1LeftMax = i == 0 ? 1<<31 : nums1[i-1];
        int nums2LeftMax = j == 0 ? 1<<31 : nums2[j-1];
        int nums1RightMin = i == m ? ~(1<<31) : nums1[i];
        int nums2RightMin = j == n ? ~(1<<31) : nums2[j];

        if ((m+n) % 2) {
            return std::max(nums1LeftMax, nums2LeftMax);
        }
        return (double)(std::max(nums1LeftMax, nums2LeftMax) + std::min(nums1RightMin, nums2RightMin)) / 2;
    }
};
```
time: O(log(min(m, n)))

space: O(1)