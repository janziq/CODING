https://github.com/fuzzywe/CODING/blob/main/ARRAYS/SORT%200s%2C1s.md

Example 1:
Input Format
: N = 3, nums[] = {3,2,3}
Result
: 3
Explanation
: When we just count the occurrences of each number and compare with half of the size of the array, you will get 3 for the above solution. 

Example 2:
Input Format:
  N = 7, nums[] = {2,2,1,1,1,2,2}

Result
: 2

Explanation
: After counting the number of times each element appears and comparing it with half of array size, we get 2 as result.

Example 3:
Input Format:
  N = 10, nums[] = {4,4,2,4,3,4,4,3,2,4}

Result
: 4

Approach 1: Sorting
Intuition:
The intuition behind this approach is that if an element occurs more than n/2 times in the array (where n is the size of the array), it will always occupy the middle position when the array is sorted. Therefore, we can sort the array and return the element at index n/2.

Explanation:
The code begins by sorting the array nums in non-decreasing order using the sort function from the C++ Standard Library. This rearranges the elements such that identical elements are grouped together.
Once the array is sorted, the majority element will always be present at index n/2, where n is the size of the array.
This is because the majority element occurs more than n/2 times, and when the array is sorted, it will occupy the middle position.
The code returns the element at index n/2 as the majority element.
The time complexity of this approach is O(n log n) since sorting an array of size n takes O(n log n) time.
```
Code
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        return nums[n/2];
    }
};
```
Approach 2: Hash Map
Intuition:
The intuition behind using a hash map is to count the occurrences of each element in the array and then identify the element that occurs more than n/2 times. By storing the counts in a hash map, we can efficiently keep track of the occurrences of each element.

Explanation:

The code begins by initializing a hash map m to store the count of occurrences of each element.
It then iterates through the array nums using a for loop.
For each element nums[i], it increments its count in the hash map m by using the line m[nums[i]]++;.
If nums[i] is encountered for the first time, it will be added to the hash map with a count of 1.
If nums[i] has been encountered before, its count in the hash map will be incremented by 1.
After counting the occurrences of each element, the code updates n to be n/2, where n is the size of the array. This is done to check if an element occurs more than n/2 times, which is the criteria for being the majority element.
The code then iterates through the key-value pairs in the hash map using a range-based for loop.
For each key-value pair (x.first, x.second), it checks if the count x.second is greater than n.
If the count is greater than n, it means that x.first occurs more than n/2 times, so it returns x.first as the majority element.
If no majority element is found in the hash map, the code returns 0 as the default value.
Note that this will only occur if the input array nums is empty or does not have a majority element.
The time complexity of this approach is O(n) because it iterates through the array once to count the occurrences and then iterates through the hash map, which has a maximum size of the number of distinct elements in the array.
```cpp
Code
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n = nums.size();
        unordered_map<int, int> m;
        
        for(int i = 0; i < n; i++){
            m[nums[i]]++;
        }
        n = n/2;
        for(auto x: m){
            if(x.second > n){
                return x.first;
            }
        }
        return 0;
    }
};
```
Approach 3: Moore Voting Algorithm
Intuition:
**The intuition behind the Moore's Voting Algorithm is based on the fact that if there is a majority element in **
**an array, it will always remain in the lead, even after encountering other elements.**

Explanation:
Algorithm:

Initialize two variables: count and candidate. Set count to 0 and candidate to an arbitrary value.
Iterate through the array nums:
a. If count is 0, assign the current element as the new candidate and increment count by 1.
b. If the current element is the same as the candidate, increment count by 1.
c. If the current element is different from the candidate, decrement count by 1.
After the iteration, the candidate variable will hold the majority element.
Explanation:

The algorithm starts by assuming the first element as the majority candidate and sets the count to 1.
As it iterates through the array, it compares each element with the candidate:
a. If the current element matches the candidate, it suggests that it reinforces the majority element because it appears again. Therefore, the count is incremented by 1.
b. If the current element is different from the candidate, it suggests that there might be an equal number of occurrences of the majority element and other elements. Therefore, the count is decremented by 1.
Note that decrementing the count doesn't change the fact that the majority element occurs more than n/2 times.
If the count becomes 0, it means that the current candidate is no longer a potential majority element. In this case, a new candidate is chosen from the remaining elements.
The algorithm continues this process until it has traversed the entire array.
The final value of the candidate variable will hold the majority element.
Explanation of Correctness:
The algorithm works on the basis of the assumption that the majority element occurs more than n/2 times in the array. This assumption guarantees that even if the count is reset to 0 by other elements, the majority element will eventually regain the lead.

Let's consider two cases:

If the majority element has more than n/2 occurrences:

The algorithm will ensure that the count remains positive for the majority element throughout the traversal, guaranteeing that it will be selected as the final candidate.
If the majority element has exactly n/2 occurrences:

In this case, there will be an equal number of occurrences for the majority element and the remaining elements combined.
However, the majority element will still be selected as the final candidate because it will always have a lead over any other element.
In both cases, the algorithm will correctly identify the majority element.

The time complexity of the Moore's Voting Algorithm is O(n) since it traverses the array once.

This approach is efficient compared to sorting as it requires only a single pass through the array and does not change the original order of the elements.
```cpp
Code
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count = 0;
        int candidate = 0;
        
        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            
            if (num == candidate) {
                count++;
            } else {
                count--;
            }
        }
        
        return candidate;
    }
};
```

If you are a beginner solve these problems which makes concepts clear for future coding:


Two Sum
Roman to Integer

Palindrome Number

Maximum Subarray

Remove Element

Contains Duplicate

Add Two Numbers

Majority Element

Remove Duplicates from Sorted Array

Practice them in a row for better understanding and please Upvote the post for more questions.



Aadarsh_Param_Akhouri
Jun 24, 2023
Genius Approach !!

218
Show 1 Replies
Reply

3rd approach using 'Moore Voting Algorithm' was awesome!


Let's dry run the Boyer-Moore Voting Algorithm for the `majorityElement` function line by line. We'll assume the input is `nums = [3, 2, 3]`.

### Code:
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count = 0;         // Step 1: Initialize count as 0.
        int candidate = 0;     // Step 2: Initialize candidate as 0.
        
        for (int num : nums) { // Step 3: Loop through each number in nums.
            if (count == 0) {  // Step 4: If count is 0, set current num as candidate.
                candidate = num;
            }
            
            if (num == candidate) {  // Step 5: If num matches candidate, increment count.
                count++;
            } else {                 // Step 6: Else, decrement count.
                count--;
            }
        }
        
        return candidate;      // Step 7: Return the candidate as the majority element.
    }
};
```

### Dry Run for `nums = [3, 2, 3]`

- **Initial State**:  
  `count = 0`, `candidate = 0`.

---

#### First Iteration (`num = 3`):
1. `for (int num : nums)` → The loop starts with `num = 3`.
2. `if (count == 0)` → Since `count` is 0, `candidate = 3`.  
   *Now*: `candidate = 3`, `count = 0`.
3. `if (num == candidate)` → `3 == 3`, so increment `count`.  
   *Now*: `candidate = 3`, `count = 1`.

---

#### Second Iteration (`num = 2`):
1. `for (int num : nums)` → The loop continues with `num = 2`.
2. `if (count == 0)` → `count` is 1, so this block is skipped.
3. `if (num == candidate)` → `2 != 3`, so decrement `count`.  
   *Now*: `candidate = 3`, `count = 0`.

---

#### Third Iteration (`num = 3`):
1. `for (int num : nums)` → The loop continues with `num = 3`.
2. `if (count == 0)` → Since `count` is 0, `candidate = 3`.  
   *Now*: `candidate = 3`, `count = 0`.
3. `if (num == candidate)` → `3 == 3`, so increment `count`.  
   *Now*: `candidate = 3`, `count = 1`.

---

### End of Loop:
- The loop is finished, and the function returns `candidate = 3`.

### Final Output:
- The majority element is `3`.

### Summary:
- **First Iteration**: `candidate = 3`, `count = 1` (3 becomes the candidate).
- **Second Iteration**: `candidate = 3`, `count = 0` (count decreases since 2 is not the candidate).
- **Third Iteration**: `candidate = 3`, `count = 1` (3 is reaffirmed as the majority element).

### Time Complexity:
- **O(n)**: Each element in the array is visited once.

### Space Complexity:
- **O(1)**: Only a few variables are used (count and candidate).
