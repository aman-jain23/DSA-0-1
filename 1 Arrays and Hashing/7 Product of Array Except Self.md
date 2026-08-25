## Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i]. 
### The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer. 
### You must write an algorithm that runs in O(n) time and without using the division operation.

```
Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```
```
Example 2:

Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```
```
Constraints:

2 <= nums.length <= 105
-30 <= nums[i] <= 30
The input is generated such that answer[i] is guaranteed to fit in a 32-bit integer.
```
## 1. Brute Force
```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];

        for (int i = 0; i < n; i++) {
            int prod = 1;
            for (int j = 0; j < n; j++) {
                if (i != j) {
                    prod *= nums[j];
                }
            }
            res[i] = prod;
        }
        return res;
    }
}
```
<img width="786" height="237" alt="image" src="https://github.com/user-attachments/assets/33344917-423d-4d74-a053-c72354773e7a" />

## 2. Division
```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int prod = 1, zeroCount = 0;
        for (int num : nums) {
            if (num != 0) {
                prod *= num;
            } else {
                zeroCount++;
            }
        }

        if (zeroCount > 1) {
            return new int[nums.length];
        }

        int[] res = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            if (zeroCount > 0) {
                res[i] = (nums[i] == 0) ? prod : 0;
            } else {
                res[i] = prod / nums[i];
            }
        }
        return res;
    }
}
```
<img width="781" height="242" alt="image" src="https://github.com/user-attachments/assets/a9cd3ce4-16ca-4764-b1e7-1fa71aa4e0d9" />

## 3. Prefix & Suffix
```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];
        int[] pref = new int[n];
        int[] suff = new int[n];

        pref[0] = 1;
        suff[n - 1] = 1;
        for (int i = 1; i < n; i++) {
            pref[i] = nums[i - 1] * pref[i - 1];
        }
        for (int i = n - 2; i >= 0; i--) {
            suff[i] = nums[i + 1] * suff[i + 1];
        }
        for (int i = 0; i < n; i++) {
            res[i] = pref[i] * suff[i];
        }
        return res;
    }
}
```
<img width="703" height="167" alt="image" src="https://github.com/user-attachments/assets/999ca85f-2b7c-4fb1-bbe9-345801c639af" />

## 4. Prefix & Suffix (Optimal)
```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];

        res[0] = 1;
        for (int i = 1; i < n; i++) {
            res[i] = res[i - 1] * nums[i - 1];
        }

        int postfix = 1;
        for (int i = n - 1; i >= 0; i--) {
            res[i] *= postfix;
            postfix *= nums[i];
        }
        return res;
    }
}
```
<img width="746" height="252" alt="image" src="https://github.com/user-attachments/assets/56da0f6f-2c0a-40f4-a29a-0a394e6e06fa" />
