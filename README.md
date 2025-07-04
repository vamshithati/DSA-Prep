# DSA-Prep
# 100 Days of DSA Prep - Day 1

## Arrays Fundamentals

Welcome to Day 1 of my 100-day Data Structures and Algorithms (DSA) preparation journey! Today's focus was on understanding the basics of arrays and tackling two fundamental problems.

### Problems Solved:

1.  **Two Sum**
    * **Description:** Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.
    * **Approach:** (Briefly explain your approach, e.g., "Used a hash map to store elements and their indices for efficient lookup.")
    * **Time Complexity:** O(N) (if using hash map)
    * **Space Complexity:** O(N) (if using hash map)
    * https://leetcode.com/problems/two-sum/submissions/1682807529

2.  **Contains Duplicate**
    * **Description:** Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.
    * **Approach:** (Briefly explain your approach, e.g., "Used a hash set to store encountered numbers and check for duplicates.")
    * **Time Complexity:** O(N) (if using hash set/map, as each element is inserted/checked once)
    * **Space Complexity:** O(N) (in the worst case, if all elements are distinct and stored in the hash set)
    * https://leetcode.com/problems/contains-duplicate/submissions/1682863242

### What I Learned Today:

* Refreshed my understanding of array properties and operations.
* Practiced identifying optimal approaches for common array problems.
* Gained hands-on experience with hash maps/dictionaries/sets for efficient lookup and tracking.

### Looking Forward:

Excited for Day 2 and continuing to build a strong foundation in DSA!

100 Days of DSA Prep - Day 2
Arrays - Continued Practice with LeetCode
Day 2 was dedicated to solidifying my understanding of arrays by tackling several common LeetCode problems. These challenges provided hands-on experience with different array manipulation techniques and helped me practice optimizing for both time and space complexity using JavaScript.

Problems Solved:
1. LeetCode 485: Max Consecutive Ones
Description: Given a binary array nums, return the maximum number of consecutive 1's in the array.

My Code:

var findMaxConsecutiveOnes = function(nums) {
    let res = 0;   // Stores the maximum consecutive ones I've found so far
    let count = 0; // Tracks the current sequence of consecutive ones

   // Iterate through each element in the array
    for (let i = 0; i < nums.length; i++){
        if (nums[i] === 1){
            count++; // If current element is 1, I increment the current count
        }
        else{
            // If current element is 0, the sequence of 1s is broken
            res = Math.max(res, count); // I update the maximum result with the current count
            count = 0;                 // I reset current count for a new sequence
        }
    }
    // Important: After the loop, I check one last time.
    // This handles cases where the array ends with 1s (e.g., [1,1,0,1,1,1])
    res = Math.max(res, count);
    return res;
};

Explanation:
This solution efficiently finds the maximum consecutive ones using a single pass. I maintain two variables: count for the current streak of ones and res for the overall maximum streak. When a 1 is encountered, count increments. When a 0 is found, it signifies the end of a sequence of 1s, so res is updated with the maximum of its current value and count, and count is reset. A crucial final Math.max(res, count) after the loop ensures that if the array ends with 1s, that final sequence's length is also considered for the maximum.

Time Complexity: O(N) - A single pass through the array.

Space Complexity: O(1) - I used a constant amount of extra space.



2. LeetCode 283: Move Zeroes
Description: Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

My Code:

var moveZeroes = function(nums) {
    let prev = 0; // This pointer tracks the position where the next non-zero element should be placed

   // Iterate through the array with 'i'
    for(let i = 0; i < nums.length; i++){
        if(nums[i] !== 0){ // If the current element (at 'i') is non-zero
            // I swap the current non-zero element with the element at 'prev' position
            // This effectively moves non-zero elements to the front
            let temp = nums[prev];
            nums[prev] = nums[i];
            nums[i] = temp;
            prev++; // I increment 'prev' to point to the next position for a non-zero element
        }
        // If nums[i] is 0, I simply skip it. The 'prev' pointer stays put,
        // waiting for the next non-zero element to swap with this 0.
    }
};

Explanation:
This solution uses an efficient in-place two-pointer approach. The prev pointer (often called nonZeroPointer or insertPosition) keeps track of the next available slot for a non-zero element, starting from the beginning of the array. The i pointer iterates through the entire array. If nums[i] is non-zero, it's swapped with nums[prev], and prev is incremented. If nums[i] is zero, i simply moves on. This process effectively pushes all non-zero elements to the front while preserving their relative order, naturally leaving all zeroes at the end.

Time Complexity: O(N) - A single pass through the array.

Space Complexity: O(1) - I modified the array in-place without using extra space.



3. LeetCode 977: Squares of a Sorted Array
Description: Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

My Code:

var sortedSquares = function(nums) {
    let left = 0;                 // Pointer at the beginning of the input array
    let right = nums.length - 1;  // Pointer at the end of the input array
    let result = [];              // The array to store the squared and sorted numbers
    // Pointer for placing elements into the 'result' array, starting from the end
    let position = nums.length - 1;
   
   // Continue as long as the left pointer is less than or equal to the right pointer
    while( left <= right ){
        // I compare the squares of the elements at the left and right pointers
        if(nums[left] ** 2 > nums[right] ** 2 ){
            // If the square of the left element is greater, it's the largest current square
            result[position] = nums[left] ** 2; // I place it at the current 'position' in result
            position--;                         // I move result pointer backward
            left++;                             // I move left input pointer forward
        }
        else{
            // Otherwise (square of right element is greater or equal), it's the largest current square
            result[position] = nums[right] ** 2; // I place it at the current 'position' in result
            position--;                          // I move result pointer backward
            right--;                             // I move right input pointer backward
        }
    }
    return result; // I return the newly formed sorted array of squares
};

Explanation:
This problem leverages the fact that the original array is sorted. The crucial insight is that the largest squared values will always come from either the largest positive number or the smallest negative number (which becomes a large positive when squared). This solution uses two pointers, left and right, starting at the ends of the input array. It also uses a position pointer to fill the result array from its end backwards. In each step, I compare the squares of nums[left] and nums[right]. The larger squared value is placed at result[position], and the corresponding pointer (left or right) is moved inward, and position is decremented. This ensures the result array is built in sorted (non-decreasing) order.

Time Complexity: O(N) - A single pass through the array.

Space Complexity: O(N) - For the new result array.



Key Takeaways from Day 2:
Mastered Two-Pointer Technique: I applied the two-pointer approach effectively in multiple scenarios, including in-place modification (Move Zeroes) and generating sorted output from a sorted input (Squares of a Sorted Array). This technique is incredibly versatile for array problems and often leads to optimal time and space complexity.

In-Place Optimization: I gained a deeper understanding of how to modify arrays without allocating significant extra space, which is crucial for optimizing memory usage, especially for large datasets.

Leveraging Array Properties: I learned to capitalize on the inherent properties of input arrays (e.g., sorted arrays) to devise more efficient algorithms than brute-force approaches (e.g., avoiding a full sort after squaring, which would be O(N log N)).

Iterative State Management: I refined my ability to manage state variables (count, res, prev, left, right, position) effectively within iterative solutions to keep track of progress and results.

JavaScript Array Methods: I reinforced the use of basic JavaScript array manipulation and Math.max for efficient comparisons.

Looking Forward:
Feeling more confident with array manipulations and excited to tackle new data structures and algorithms on Day 3!
