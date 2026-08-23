## You are given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target. 
## You may assume that each input would have exactly one solution, and you may not use the same element twice. 
## You can return the answer in any order.
```
Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
```
Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]
```
```
Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
```
```
Constraints:

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.
```

## 1. Brute Force
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[0];
    }
}
```
<img width="652" height="177" alt="image" src="https://github.com/user-attachments/assets/6a87d828-3889-4f60-bce5-e99221b07357" />

## 2. Sorting
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[][] A = new int[nums.length][2];
        for (int i = 0; i < nums.length; i++) {
            A[i][0] = nums[i];
            A[i][1] = i;
        }

        Arrays.sort(A, Comparator.comparingInt(a -> a[0]));

        int i = 0, j = nums.length - 1;
        while (i < j) {
            int cur = A[i][0] + A[j][0];
            if (cur == target) {
                return new int[]{Math.min(A[i][1], A[j][1]),
                                 Math.max(A[i][1], A[j][1])};
            } else if (cur < target) {
                i++;
            } else {
                j--;
            }
        }
        return new int[0];
    }
}
```
<img width="721" height="181" alt="image" src="https://github.com/user-attachments/assets/acf79598-0e53-4e15-9861-6de7c89d1795" />

## 3. Hash Map (Two Pass)
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> indices = new HashMap<>();  // val -> index

        for (int i = 0; i < nums.length; i++) {
            indices.put(nums[i], i);
        }

        for (int i = 0; i < nums.length; i++) {
            int diff = target - nums[i];
            if (indices.containsKey(diff) && indices.get(diff) != i) {
                return new int[]{i, indices.get(diff)};
            }
        }

        return new int[0];
    }
}
```
<img width="694" height="195" alt="image" src="https://github.com/user-attachments/assets/6f292fa4-3bd1-4919-bbf9-8fdb60c9baec" />

## 4. Hash Map (One Pass)
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> prevMap = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            int diff = target - num;

            if (prevMap.containsKey(diff)) {
                return new int[] { prevMap.get(diff), i };
            }

            prevMap.put(num, i);
        }

        return new int[] {};
    }
}
```
<img width="728" height="183" alt="image" src="https://github.com/user-attachments/assets/e3268cfc-e040-4bdf-bd40-5dd67bf3c958" />


