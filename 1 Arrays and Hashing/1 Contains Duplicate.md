## Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.
```
Example 1:
Input: nums = [1,2,3,1]
Output: true
Explanation: The element 1 occurs at the indices 0 and 3.
```
```
Example 2:
Input: nums = [1,2,3,4]
Output: false
Explanation: All elements are distinct.
```
```
Example 3:
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

## 1. Brute Force
```
public class Solution {
    public boolean hasDuplicate(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] == nums[j]) {
                    return true;
                }
            }
        }
        return false;
    }
}
```
<img width="407" height="189" alt="image" src="https://github.com/user-attachments/assets/5529e5cb-9418-42cb-ae36-16fe764d0165" />

## 2. Sorting
```
public class Solution {
    public boolean hasDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) {
                return true;
            }
        }
        return false;
    }
}
```

<img width="706" height="212" alt="image" src="https://github.com/user-attachments/assets/b81a1872-947c-42ca-b5fb-59a1431bb845" />

## 3. Hash Set

```
public class Solution {
    public boolean hasDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return true;
            }
            seen.add(num);
        }
        return false;
    }
}
```
<img width="426" height="212" alt="image" src="https://github.com/user-attachments/assets/653f856e-9c59-4fda-8d93-8104447bed04" />

## 4. Hash Set Length

```
public class Solution {
    public boolean hasDuplicate(int[] nums) {
        return Arrays.stream(nums).distinct().count() < nums.length;
    }
}
```

<img width="459" height="208" alt="image" src="https://github.com/user-attachments/assets/0924f847-64c3-4742-ab07-a26454014c5b" />
