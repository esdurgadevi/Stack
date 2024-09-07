# Stack
### 2696. Minimum String Length After Removing Substrings
[Leetcode link](https://leetcode.com/problems/minimum-string-length-after-removing-substrings/submissions/1382233984?envType=problem-list-v2&envId=stack&status=TO_DO&difficulty=EASY)
<br>
You are given a string s consisting only of uppercase English letters. You can apply some operations to this string where, in one operation, you can remove any occurrence of one of the substrings "AB" or "CD" from s. Return the minimum possible length of the resulting string that you can obtain. Note that the string concatenates after removing the substring and could produce new "AB" or "CD" substrings.

Example 1:
Input: s = "ABFCACDB"
Output: 2
Explanation: We can do the following operations:
- Remove the substring "ABFCACDB", so s = "FCACDB".
- Remove the substring "FCACDB", so s = "FCAB".
- Remove the substring "FCAB", so s = "FC".
So the resulting length of the string is 2.
It can be shown that it is the minimum length that we can obtain.

Example 2:
Input: s = "ACBBD"
Output: 5
Explanation: We cannot do any operations on the string so the length remains the same.

Constraints:
1 <= s.length <= 100
s consists only of uppercase English letters.

```java
class Solution {
    public int minLength(String s) {
        Stack<Character> str = new Stack<>();
        for(int i=0;i<s.length();i++)
        {
            if(s.charAt(i)=='B')
            {
                if(!str.empty())
                {
                    char ch = str.peek();
                    if(ch=='A') str.pop();
                    else str.push(s.charAt(i));
                }
                else str.push(s.charAt(i));
            }
            else if(s.charAt(i)=='D')
            {
                if(!str.empty())
                {
                    char ch = str.peek();
                    if(ch=='C') str.pop();
                    else str.push(s.charAt(i));
                }
                else str.push(s.charAt(i));
            }
            else str.push(s.charAt(i));
        }
        return str.size();
    }
}
```
### 1544. Make The String Great
[Leetcode link](https://leetcode.com/problems/make-the-string-great/submissions/1382327628?envType=problem-list-v2&envId=stack&status=TO_DO&difficulty=EASY)
<br>
Given a string s of lower and upper case English letters. A good string is a string which doesn't have two adjacent characters s[i] and s[i + 1] where: 0 <= i <= s.length - 2
s[i] is a lower-case letter and s[i + 1] is the same letter but in upper-case or vice-versa.
To make the string good, you can choose two adjacent characters that make the string bad and remove them. You can keep doing this until the string becomes good.
Return the string after making it good. The answer is guaranteed to be unique under the given constraints.
Notice that an empty string is also good.

Example 1:
Input: s = "leEeetcode"
Output: "leetcode"
Explanation: In the first step, either you choose i = 1 or i = 2, both will result "leEeetcode" to be reduced to "leetcode".

Example 2:
Input: s = "abBAcC"
Output: ""
Explanation: We have many possible scenarios, and all lead to the same answer. For example:
"abBAcC" --> "aAcC" --> "cC" --> ""
"abBAcC" --> "abBA" --> "aA" --> ""

Example 3:
Input: s = "s"
Output: "s"

Constraints:
1 <= s.length <= 100
s contains only lower and upper case English letters.

```java
class Solution {
    public String makeGood(String s) {
        if(s.length()==0) return s;
        Stack<Character> ans = new Stack<>();
        ans.push(s.charAt(0));
        for(int i=1;i<s.length();i++)
        {
            if(ans.empty()) ans.push(s.charAt(i));
            else if(Character.toUpperCase(s.charAt(i))==Character.toUpperCase(ans.peek()))
            {
                if(Character.isUpperCase(s.charAt(i)) ^ Character.isUpperCase(ans.peek()))
                {
                    ans.pop();
                }
                else ans.push(s.charAt(i));
            }
            else ans.push(s.charAt(i));
        }
        StringBuilder res = new StringBuilder();
        while(!ans.empty())
        {
            res.append(ans.pop());
        }
        res.reverse();
        return res.toString();
    }
}
```
