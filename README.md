# Stack
### Stack implementation using array
```java
class stack {
    int size = 10000;
    int arr[] = new int[size];
    int top = -1;
    void push(int x) {
        top++;
        arr[top] = x;
    }
    int pop() {
        int x = arr[top];
        top--;
        return x;
    }
    int top() {
        return arr[top];
    }
    int size() {
        return top + 1;
    }
}
```
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
### 20. Valid Parentheses
[Leetcode link](https://leetcode.com/problems/valid-parentheses/)
<br>
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. An input string is valid if:Open brackets must be closed by the same type of brackets. Open brackets must be closed in the correct order. Every close bracket has a corresponding open bracket of the same type.
 
Example 1:
Input: s = "()"
Output: true

Example 2:
Input: s = "()[]{}"
Output: true

Example 3:
Input: s = "(]"
Output: false

Example 4:
Input: s = "([])"
Output: true

Constraints:
1 <= s.length <= 104
s consists of parentheses only '()[]{}'.

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> ans = new Stack<>();
        ans.push(s.charAt(0));
        for(int i=1;i<s.length();i++)
        {
            if(s.charAt(i)==')' && !ans.isEmpty()) 
            {
                if(ans.peek()=='(') ans.pop();
                else ans.push(s.charAt(i));
            }
            else if(s.charAt(i)==']' && !ans.isEmpty())
            {
                if(ans.peek()=='[') ans.pop();
                else ans.push(s.charAt(i));
            }
            else if(s.charAt(i)=='}' && !ans.isEmpty())
            {
                if(ans.peek()=='{') ans.pop();
                else ans.push(s.charAt(i));
            }
            else ans.push(s.charAt(i));
        }
        return ans.isEmpty();
    }
}
```
- In this cde we check the valid parantheses each parenthesis have the corrosponding parentheses if it is valid.
- The idea is first we push the first element to the stack.
- Then traverse through the full string. If the character is a open parenthesis then we simply insert the stack.
- Other wise that is close parenthesis we check the peek element of the stack if it both are same pair of group we pop the the stack element otherwise we add the current character to the stack.
- finally if the stack is empty then all parenthesis are paired so return true otherwise we return false.
### 155. Min Stack
[Leetcode link](https://leetcode.com/problems/min-stack/description/)
<br>
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.mplement the MinStack class:
MinStack() initializes the stack object.
void push(int val) pushes the element val onto the stack.
void pop() removes the element on the top of the stack.
int top() gets the top element of the stack.
int getMin() retrieves the minimum element in the stack.
You must implement a solution with O(1) time complexity for each function.

Example 1:
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]
Output
[null,null,null,null,-3,null,0,-2]
Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2

Constraints:
-231 <= val <= 231 - 1
Methods pop, top and getMin operations will always be called on non-empty stacks.
At most 3 * 104 calls will be made to push, pop, top, and getMin.

```java
class MinStack {
    int top;
    int[] arr;
    public MinStack() {
        arr = new int[10000];
        top = -1;
    }
    public void push(int val) {
        arr[++top] = val;
    }
    public void pop() {
        top--;
    }
    public int top() {
        return arr[top];
    }
    public int getMin() {
        int min = Integer.MAX_VALUE;
        for(int i=0;i<=top;i++)
        {
            min = Math.min(min,arr[i]);
        }
        return min;
    }
}
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
### Infix to Postfix
[Geeks for Geeks](https://www.geeksforgeeks.org/problems/infix-to-postfix-1587115620/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=infix-to-postfix)
<br>
Example 1:
Input: str = "a+b*(c^d-e)^(f+g*h)-i"
Output: abcd^e-fgh*+^*+i-
Explanation:
After converting the infix expression 
into postfix expression, the resultant 
expression will be abcd^e-fgh*+^*+i-

Example 2:
Input: str = "A*(B+C)/D"
Output: ABC+*D/
Explanation:
After converting the infix expression 
into postfix expression, the resultant 
expression will be ABC+*D/

```java
class Solution {
    // Function to convert an infix expression to a postfix expression.
    public static int pre(char ch)
    {
        if(ch=='^') return 3;
        else if(ch=='*' || ch=='/') return 2;
        else if(ch=='+' || ch=='-') return 1;
        else return -1;
    }
    public static String infixToPostfix(String exp) {
        Stack<Character> ans = new Stack<>();
        StringBuilder str = new StringBuilder();
        for(int i=0;i<exp.length();i++)
        {
            char ch = exp.charAt(i);
            if(Character.isLetterOrDigit(ch))
            {
                str.append(ch);
            }
            else if(ch=='(') ans.push(ch);
            else if(ch==')')
            {
                while(!ans.isEmpty() && ans.peek()!='(')
                {
                    str.append(ans.pop());
                }
                ans.pop();
            }
            else 
            {
                while(!ans.isEmpty() && pre(ch)<pre(ans.peek()))
                {
                    str.append(ans.pop());
                }
                ans.push(ch);
            }
        }
        while(!ans.isEmpty()) 
        {
            str.append(ans.pop());
        }
        return str.toString();
    }
}
```
- Convert the infix to postfix expression is very easy.
- First we create a stack and the string which holds the postfix expression.
- Whenever we see the alphabet or digit then we append the character to string.
- If we see the open parenthesis we'(' we push to the stack.
- If we see the close parenthesis then we append the operator between the open and close parenthesis to the string.
- If we see other operator if the priority is greater than the priority of the stack operator then we push it into stack or else we take the operator from the stack and add it to the string. untill the priority will greater than the stack element priority.
- Finally we add all the stack operator to the string.
### 682. Baseball Game
[Leetcode link](https://leetcode.com/problems/baseball-game/?envType=problem-list-v2&envId=stack&status=TO_DO&difficulty=EASY)
<br>
You are keeping the scores for a baseball game with strange rules. At the beginning of the game, you start with an empty record.
You are given a list of strings operations, where operations[i] is the ith operation you must apply to the record and is one of the following:
An integer x.
Record a new score of x.
'+'.
Record a new score that is the sum of the previous two scores.
'D'.
Record a new score that is the double of the previous score.
'C'.
Invalidate the previous score, removing it from the record.
Return the sum of all the scores on the record after applying all the operations.
The test cases are generated such that the answer and all intermediate calculations fit in a 32-bit integer and that all operations are valid.

Example 1:
Input: ops = ["5","2","C","D","+"]
Output: 30
Explanation:
"5" - Add 5 to the record, record is now [5].
"2" - Add 2 to the record, record is now [5, 2].
"C" - Invalidate and remove the previous score, record is now [5].
"D" - Add 2 * 5 = 10 to the record, record is now [5, 10].
"+" - Add 5 + 10 = 15 to the record, record is now [5, 10, 15].
The total sum is 5 + 10 + 15 = 30.

Example 2:
Input: ops = ["5","-2","4","C","D","9","+","+"]
Output: 27
Explanation:
"5" - Add 5 to the record, record is now [5].
"-2" - Add -2 to the record, record is now [5, -2].
"4" - Add 4 to the record, record is now [5, -2, 4].
"C" - Invalidate and remove the previous score, record is now [5, -2].
"D" - Add 2 * -2 = -4 to the record, record is now [5, -2, -4].
"9" - Add 9 to the record, record is now [5, -2, -4, 9].
"+" - Add -4 + 9 = 5 to the record, record is now [5, -2, -4, 9, 5].
"+" - Add 9 + 5 = 14 to the record, record is now [5, -2, -4, 9, 5, 14].
The total sum is 5 + -2 + -4 + 9 + 5 + 14 = 27.

Example 3:
Input: ops = ["1","C"]
Output: 0
Explanation:
"1" - Add 1 to the record, record is now [1].
"C" - Invalidate and remove the previous score, record is now [].
Since the record is empty, the total sum is 0.
 
Consraints:
1 <= operations.length <= 1000
operations[i] is "C", "D", "+", or a string representing an integer in the range [-3 * 104, 3 * 104].
For operation "+", there will always be at least two previous scores on the record.
For operations "C" and "D", there will always be at least one previous score on the record.

```java
class Solution {
    public int calPoints(String[] operations) {
        Stack<Integer> stk = new Stack<>();
        int sum = 0;
        for(String s:operations)
        {
            if(s.equals("C")) stk.pop();
            else if(s.equals("D")) stk.push(stk.peek()*2);
            else if(s.equals("+"))
            {
                int t1 = stk.peek();
                stk.pop();
                int t2 = stk.peek();
                stk.push(t1);
                stk.push(t1+t2);
            }
            else stk.push(Integer.parseInt(s));
        }
        for(int x:stk) sum+=x;
        return sum;
    }
}
```
### 844. Backspace String Compare
[leetcode link](https://leetcode.com/problems/backspace-string-compare/description/?envType=problem-list-v2&envId=stack&status=TO_DO&difficulty=EASY)
<br>
Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.
Note that after backspacing an empty text, the text will continue empty.

Example 1:
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".

Example 2:
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".

Example 3:
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".

Constraints:
1 <= s.length, t.length <= 200
s and t only contain lowercase letters and '#' characters.

```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        Stack<Character> a1 = new Stack<>();
        Stack<Character> a2 = new Stack<>();
        for(int i=0;i<s.length();i++)
        {
            if(s.charAt(i)=='#') 
            {
                if(!a1.isEmpty()) a1.pop();
            }
            else if(s.charAt(i)!='#') a1.push(s.charAt(i));
        }
        for(int i=0;i<t.length();i++)
        {
            if(t.charAt(i)=='#') 
            {
                if(!a2.isEmpty()) a2.pop();
            }
            else if(t.charAt(i)!='#') a2.push(t.charAt(i));
        }
        System.out.print(a1.size()+" "+a2.size());
        if(a1.size()!=a2.size()) 
        {
            return false;
        }
        while(!a1.isEmpty() && !a2.isEmpty())
        {
            if(a1.peek()!=a2.peek()) return false;
            a1.pop();
            a2.pop();
        }
        return true;
    }
}
```
- In this code we push the character if it is alpabet. Otherwise we pop the previous stack element finally we check the equallyty of the two stack.
