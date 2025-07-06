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

# 100 Days of DSA Prep - Day 2
Arrays - Continued Practice with LeetCode
Day 2 was dedicated to solidifying my understanding of arrays by tackling several common LeetCode problems. These challenges provided hands-on experience with different array manipulation techniques and helped me practice optimizing for both time and space complexity using JavaScript.

Problems Solved:

### 1. LeetCode 485: Max Consecutive Ones

Description: Given a binary array nums, return the maximum number of consecutive 1's in the array.


```javascript
var findMaxConsecutiveOnes = function(nums) {
    let res = 0; // Stores the maximum consecutive ones I've found so far
    let count = 0; // Tracks the current sequence of consecutive ones

    // Iterate through each element in the array
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === 1) {
            count++; // If current element is 1, increment the current count
        } else {
            // If current element is 0, the sequence of 1s is broken
            res = Math.max(res, count); // Update the maximum result with the current count
            count = 0; // Reset current count for a new sequence
        }
    }

    // Important: After the loop, check one last time.
    // This handles cases where the array ends with 1s (e.g., [1,1,0,1,1,1])
    res = Math.max(res, count);

    return res;
};
```

**Explanation:**

This solution efficiently finds the maximum consecutive ones using a single pass. I maintain two variables: count for the current streak of ones and res for the overall maximum streak. When a 1 is encountered, count increments. When a 0 is found, it signifies the end of a sequence of 1s, so res is updated with the maximum of its current value and count, and count is reset. A crucial final Math.max(res, count) after the loop ensures that if the array ends with 1s, that final sequence's length is also considered for the maximum.

Time Complexity: O(N) - A single pass through the array.

Space Complexity: O(1) - I used a constant amount of extra space.

### 

### 2. LeetCode 283: Move Zeroes

Description: Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

```javascript
var moveZeroes = function(nums) {
    let prev = 0; // This pointer tracks the position where the next non-zero element should be placed

    // Iterate through the array with 'i'
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== 0) {
            // If the current element (at 'i') is non-zero
            // Swap the current non-zero element with the element at 'prev' position
            // This effectively moves non-zero elements to the front
            let temp = nums[prev];
            nums[prev] = nums[i];
            nums[i] = temp;

            prev++; // Increment 'prev' to point to the next position for a non-zero element
        }
        // If nums[i] is 0, simply skip it.
        // The 'prev' pointer stays put, waiting for the next non-zero element to swap with this 0.
    }
};
```


**Explanation:**

This solution uses an efficient in-place two-pointer approach. The prev pointer (often called nonZeroPointer or insertPosition) keeps track of the next available slot for a non-zero element, starting from the beginning of the array. The i pointer iterates through the entire array. If nums[i] is non-zero, it's swapped with nums[prev], and prev is incremented. If nums[i] is zero, i simply moves on. This process effectively pushes all non-zero elements to the front while preserving their relative order, naturally leaving all zeroes at the end.

Time Complexity: O(N) - A single pass through the array.

Space Complexity: O(1) - I modified the array in-place without using extra space.



### 3. LeetCode 977: Squares of a Sorted Array

Description: Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

```javascript
var sortedSquares = function(nums) {
    let left = 0;                 // Pointer at the beginning of the input array
    let right = nums.length - 1;  // Pointer at the end of the input array
    let result = [];              // The array to store the squared and sorted numbers

    // Pointer for placing elements into the 'result' array, starting from the end
    let position = nums.length - 1;

    // Continue as long as the left pointer is less than or equal to the right pointer
    while (left <= right) {
        // Compare the squares of the elements at the left and right pointers
        if (nums[left] ** 2 > nums[right] ** 2) {
            // If the square of the left element is greater, it's the largest current square
            result[position] = nums[left] ** 2; // Place it at the current 'position' in result
            position--;                         // Move result pointer backward
            left++;                             // Move left input pointer forward
        } else {
            // Otherwise (square of right element is greater or equal), it's the largest current square
            result[position] = nums[right] ** 2; // Place it at the current 'position' in result
            position--;                          // Move result pointer backward
            right--;                             // Move right input pointer backward
        }
    }

    return result; // Return the newly formed sorted array of squares
};
```

**Explanation:**

This problem leverages the fact that the original array is sorted. The crucial insight is that the largest squared values will always come from either the largest positive number or the smallest negative number (which becomes a large positive when squared). This solution uses two pointers, left and right, starting at the ends of the input array. It also uses a position pointer to fill the result array from its end backwards. In each step, I compare the squares of nums[left] and nums[right]. The larger squared value is placed at result[position], and the corresponding pointer (left or right) is moved inward, and position is decremented. This ensures the result array is built in sorted (non-decreasing) order.

Time Complexity: O(N) - A single pass through the array.

Space Complexity: O(N) - For the new result array.



**Key Takeaways from Day 2:**

Mastered Two-Pointer Technique: I applied the two-pointer approach effectively in multiple scenarios, including in-place modification (Move Zeroes) and generating sorted output from a sorted input (Squares of a Sorted Array). This technique is incredibly versatile for array problems and often leads to optimal time and space complexity.

In-Place Optimization: I gained a deeper understanding of how to modify arrays without allocating significant extra space, which is crucial for optimizing memory usage, especially for large datasets.

Leveraging Array Properties: I learned to capitalize on the inherent properties of input arrays (e.g., sorted arrays) to devise more efficient algorithms than brute-force approaches (e.g., avoiding a full sort after squaring, which would be O(N log N)).

Iterative State Management: I refined my ability to manage state variables (count, res, prev, left, right, position) effectively within iterative solutions to keep track of progress and results.

JavaScript Array Methods: I reinforced the use of basic JavaScript array manipulation and Math.max for efficient comparisons.

Looking Forward:
Feeling more confident with array manipulations and excited to tackle new data structures and algorithms on Day 3!



# 100 Days of DSA Prep - Day 3

## Arrays - More In-place Manipulation and Counting

Day 3 continued my journey with arrays, focusing on problems that required careful in-place modifications and efficient counting strategies. I tackled two interesting LeetCode problems that helped me refine my understanding of array operations and number properties.

---

### Problems Solved:

#### 1. LeetCode 1089: Duplicate Zeros

* **Description:** Given a fixed-length integer array `arr`, I needed to duplicate each occurrence of zero, shifting the remaining elements to the right. Elements beyond the original length of the array were not to be written. This meant modifying the array in-place.


    ```javascript
    var duplicateZeros = function(arr) {
        // I iterate through the array
        for(let i = 0; i < arr.length; i++){
            // If I find a zero
            if( arr[i] === 0) {
                // I use splice to insert another zero right after the current one.
                // This shifts all subsequent elements to the right.
                arr.splice(i, 0, 0);
                // Since the array's length increased, I remove the last element
                // to maintain the original fixed length constraint.
                arr.pop();
                // I increment 'i' again to skip the newly inserted zero.
                // This is crucial to avoid an infinite loop (re-processing the new zero)
                // and to ensure I don't skip the element that was originally next.
                i++;
            }
        }
    };
    ```

* **Explanation:**
    My approach for `Duplicate Zeros` involves iterating through the array and, whenever a zero is encountered, using `splice(i, 0, 0)` to insert another zero at the current position. This operation shifts all subsequent elements to the right. To maintain the fixed length of the array, I immediately `pop()` the last element. A critical part of my solution is `i++` after the `splice`. This ensures that I skip over the newly inserted zero, preventing it from being processed again (which would lead to an infinite loop or incorrect duplicates) and correctly moving to the next *original* element. While this solution is concise, I recognize that `splice` and `pop` operations can be costly on large arrays as they involve shifting elements.

* **Time Complexity:** O(N^2) - In the worst case (e.g., an array full of zeros), `splice` and `pop` operations can take O(N) time each, and these are performed within a loop that runs up to N times.

* **Space Complexity:** O(1) - I modified the array in-place, using no significant extra space.



#### 2. LeetCode 1295: Find Numbers with Even Number of Digits

* **Description:** For this problem, I needed to count how many numbers in a given array `nums` contained an even number of digits.


    ```javascript
    var findNumbers = function(nums) {
        let count = 0; // This variable will store the total count of numbers with even digits

        // I iterate through each number in the input array
        for( let i = 0; i < nums.length; i++){
            // I convert the current number to a string to easily get its length (number of digits)
            let res = nums[i].toString();
            // I check if the length of the string (number of digits) is even
            if(res.length % 2 === 0){
                count++; // If it's even, I increment my counter
            }
        }
        return count; // I return the final count
    };
    ```

* **Explanation:**
    My approach for `Find Numbers with Even Number of Digits` was straightforward and effective. I iterated through each number in the array. For each number, I converted it to a string using `toString()`. This allowed me to easily determine the number of digits by checking the `length` property of the string. I then used the modulo operator (`% 2 === 0`) to check if the length was even. If it was, I incremented a `count` variable, which I returned at the end. This method is simple to understand and implement.

* **Time Complexity:** O(N) - I perform a single pass through the array. The `toString()` operation takes time proportional to the number of digits, which is logarithmic with respect to the number's value, but practically constant for typical integer ranges.

* **Space Complexity:** O(1) - I used a constant amount of extra space for the `count` variable and temporary string conversions.



### Key Takeaways from Day 3:

* **In-Place Array Modification Challenges:** I experienced firsthand the complexities of modifying an array in-place while iterating over it, particularly with operations like `splice` and `pop`. It requires careful management of loop indices to avoid skipping elements or creating infinite loops. I learned that while `splice` is convenient, its performance implications (O(N) for each call) must be considered for overall time complexity.

* **Alternative Approaches for In-Place:** For problems like `Duplicate Zeros`, I'm now aware that more optimized O(N) solutions often involve a two-pass approach (e.g., counting zeros first, then placing elements from the end) to minimize element shifting. This is something I'll keep in mind for future similar problems.

* **Number-to-String Conversion for Digit Counting:** I found a practical way to count digits in a number by converting it to a string. This is a simple and readable method for such tasks.

* **Efficiency of Modulo Operator:** Reaffirmed the utility of the modulo operator (`%`) for quickly determining properties like evenness or oddness.

### Looking Forward:

Day 3 was a great learning experience, especially with the nuances of in-place array manipulation. I'm excited to continue building my DSA skills on Day 4!

---

# 100 Days of DSA Prep – Day 4

## Arrays – Profit Maximization and Rotations

Day 4 of my DSA journey brought more classic array problems, this time focusing on identifying optimal values and performing efficient in-place manipulations. I solved two foundational LeetCode problems that enhanced my understanding of single-pass optimizations and advanced rotation techniques.

---

### Problems Solved:

#### 1. LeetCode 121: Best Time to Buy and Sell Stock

* **Description:**  
  I needed to determine the maximum profit I could achieve by buying and selling a stock once, given an array where each element represents the price of the stock on a given day.

```javascript
function maxProfit(prices) {
    let buy = prices[0]; // Initialize 'buy' with the first price
    let profit = 0;       // Initialize max profit

    for (let i = 1; i < prices.length; i++) {
        if (prices[i] < buy) {
            // Found a better buying opportunity
            buy = prices[i];
        } else {
            // Potential selling point – update max profit if higher
            profit = Math.max(prices[i] - buy, profit);
        }
    }
    return profit;
}
```

* **Explanation:**  
  This problem is solved with a single pass through the array. I track the lowest price seen so far with the `buy` variable. As I move through the array, if I find a higher price than `buy`, I calculate the profit and update the `profit` variable if it’s greater than the current max. This approach avoids the need for nested loops and efficiently finds the optimal solution in linear time.  
  I initially had some in-place modification lines like `prices[0] = 0`, but these are unnecessary and have been removed for clarity and correctness.

* **Time Complexity:** O(N) – Single pass through the prices array  
* **Space Complexity:** O(1) – Constant extra space used  
* **Link:** [LeetCode 121 Solution](#) *(optional)*

---

#### 2. LeetCode 189: Rotate Array

* **Description:**  
  Rotate the elements of an array to the right by `k` steps. The operation must be performed in-place with O(1) extra space.

```javascript
var rotate = function(nums, k) {
    k = k % nums.length; // Normalize k for larger values

    function reverse(start, end) {
        while (start < end) {
            [nums[start], nums[end]] = [nums[end], nums[start]];
            start++;
            end--;
        }
    }

    reverse(0, nums.length - 1);   // Step 1: Reverse entire array
    reverse(0, k - 1);             // Step 2: Reverse first k elements
    reverse(k, nums.length - 1);   // Step 3: Reverse the remaining elements
};
```

* **Explanation:**  
  I used the "three-reversals" algorithm, which is a clever and efficient in-place method. First, I reverse the entire array to move the last `k` elements to the front in reverse order. Then, I reverse the first `k` elements and the remaining elements separately to restore their original order. This technique avoids using any extra space and keeps the logic concise and modular through a helper function.

* **Time Complexity:** O(N) – Each element is involved in at most one swap  
* **Space Complexity:** O(1) – No extra space used beyond a few variables  
* **Link:** [LeetCode 189 Solution](#) *(optional)*

---

### Key Takeaways from Day 4:

* **Single-Pass Optimization:**  
  Reinforced the efficiency of scanning through arrays only once for problems like profit maximization. It's all about maintaining smart state (like `buy`) while iterating.

* **In-Place Array Manipulation (Advanced):**  
  Practiced the three-reversal technique for rotating arrays – a powerful tool for modifying arrays without using additional space.

* **Understanding Algorithm Constraints:**  
  Paying attention to space and time constraints upfront helped me choose the most efficient approach. Meeting O(1) space requirements made me more mindful of in-place algorithms.

* **Importance of Helper Functions:**  
  Abstracting the `reverse()` function made the rotation logic more readable and modular – something I plan to apply more often in future problems.

---

### Looking Forward:

Day 4 was a solid reinforcement of array fundamentals and brought in more optimization patterns. Excited to explore more complex scenarios and data structures in the coming days!

