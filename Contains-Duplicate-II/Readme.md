# Contains Duplicate II

## Description
Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

Example 1:
Input: nums = [1,2,3,1], k = 3
Output: true

Example 2:
Input: nums = [1,0,1,1], k = 1
Output: true

Example 3:
Input: nums = [1,2,3,1,2,3], k = 2
Output: false

Constraints:
1. 1 <= nums.length <= 105
2. -109 <= nums[i] <= 109
3. 0 <= k <= 105

## Solutions

1. With unordered_map:
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
       std::unordered_map<int, int> duplicates;
       for(int i = 0; i < nums.size(); i++) {
            if(duplicates.contains(nums[i])) {
                if(abs(duplicates[nums[i]] - i) <= k) return true;
            }
            duplicates[nums[i]] = i;
       }
       return false;
    }
};

**Result**:
*Runtime*: 74 ms | beats 63.02%
*Memory*: 98.72 MB | beats 29.99%
*Time taken*: 11m 20s
*Complexy*: Runtime O(n); Memory O(min(n,k))

2. With unordered_set:
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
       std::unordered_set<int> duplicates;
       int i = 0;
       for(int j = 0; j < nums.size(); j++) {
            if(j - i > k){
                duplicates.erase(nums[i]);
                i++;
            }
            if(duplicates.find(nums[j]) != duplicates.end()) {
                return true;
            }
            duplicates.insert(nums[j]);
       }
       return false;
    }
};

**Result**:
*Runtime*: 84 ms | beats 26.62%
*Memory*: 93.72 MB | beats 76.08%
*Time taken*: 9m 4s
*Complexy*: Runtime O(n)(amortized); Memory O(k)
