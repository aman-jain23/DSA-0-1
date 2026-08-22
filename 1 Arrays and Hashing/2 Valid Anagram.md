## Given two strings s and t, return true if t is an anagram of s, and false otherwise.

```
Example 1:
Input: s = "anagram", t = "nagaram"
Output: true
```
```
Example 2:
Input: s = "rat", t = "car"
Output: false
```
```
Constraints:
1 <= s.length, t.length <= 5 * 104
s and t consist of lowercase English letters.
```
## 1. Sorting
```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        char[] sSort = s.toCharArray();
        char[] tSort = t.toCharArray();
        Arrays.sort(sSort);
        Arrays.sort(tSort);
        return Arrays.equals(sSort, tSort);
    }
}
```
<img width="791" height="173" alt="image" src="https://github.com/user-attachments/assets/45410402-ca14-4377-a6ec-1a04cbe08eeb" />

## 2. Hash Map
```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        HashMap<Character, Integer> countS = new HashMap<>();
        HashMap<Character, Integer> countT = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            countS.put(s.charAt(i), countS.getOrDefault(s.charAt(i), 0) + 1);
            countT.put(t.charAt(i), countT.getOrDefault(t.charAt(i), 0) + 1);
        }
        return countS.equals(countT);
    }
}
```
<img width="762" height="191" alt="image" src="https://github.com/user-attachments/assets/95102498-bac6-4639-a026-7e3ff54c6c51" />

## 3. Hash Table (Using Array)

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        int[] count = new int[26];
        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i) - 'a']++;
            count[t.charAt(i) - 'a']--;
        }

        for (int val : count) {
            if (val != 0) {
                return false;
            }
        }
        return true;
    }
}
```
<img width="763" height="196" alt="image" src="https://github.com/user-attachments/assets/aa28b22f-a27a-4e3c-82a7-7b99fe60aa8a" />
