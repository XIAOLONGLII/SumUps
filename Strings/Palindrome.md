## Palindrome
1. (easy) Check if a String is a palindrome
```html
Core: Use two pointers, from left and right to go to in the middle. 
```
```java
private boolean isPalindrome(String s) {
  ine left = 0;
  int right = s.length() - 1;
  while(left < right) {
     if(s.charAt(left) != s.charAt(right)) return false;
     left++;
     right--;
  }
  return true;
}
```
------------------------

2. (medium) find the longest palindrome substring in a string
```html
We can use the function check every substring, but that would take O(N)^3 runtime
Core: Two type of palindrome, aba, aa, one is without center, one is with. So we find both, then comparing
we first come to the center index i, then expand, to see the neighbors are satisfied become a palindrome.
if it is we keep iterating, until reach not palindrome or the boundry, then we return the substring who have been a palindomr.
then compare. 
```
```java
public String findLongestPalindrome(String s) {
  String maxPalindrome = "";
  for(int i = 0; i < s.length(); i++) {
    String oddLengthPalindrome = extend(s, i, i);
    String evenLengthPalindrome = extend(s, i, i + 1);
    if(oddLengthPalindrome > max) {
      maxPalindrome = oddLengthPalindrome;
    }
    if(evenLengthPalindrome > max) {
      maxPalindrome = evenLengthPalindrome;
    }
  }
  return maxPalindrome;
}
private String extend(String s, int left, int right) {
  while(left >=0 && right < 0 && s.charAt(left) == s.charAt(right)) {
     left--;
     right++;
  }
  return s.substring(left + 1, right)
}
```

------------------------

3. (medium) find the longest palindrome substring's length in a string

```html
The same idea of find the longest substring. 
We will store the length to max, then return it
```
```java

public static int findLongestPalindrome(String s) {
 
    int max = 0;
    for(int i = 0; i < s.length(); i++) {
      String oddLengthPalindrome = extend(s, i, i);
      String evenLengthPalindrome = extend(s, i, i + 1);
      if(oddLengthPalindrome.length() > max) {
        max = oddLengthPalindrome.length();
      }
      if(evenLengthPalindrome.length() > max) {
        max = evenLengthPalindrome.length();
      }
    }
    return max;
}
private String extends(String s, int left, int right) {
  while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
    left--;
    right++; //向左和右扩展 然后去发现palindrome
  }
  return s.substring(left + 1, right); // right is exclusive
}

```
------------------------

4. find all substrings are palindromes

```java
import java.util.*;
class allPalindromes {
  // all substring of Strings are palindrome
  public static void main(String[] args) {
    String s = "abbcbb";
    System.out.println(findPalindromes(s));
  }

  private static HashSet<String> findPalindromes(String s) {

      HashSet<String> list = new HashSet<>();
      for(int i = 0; i < s.length(); i++) {
        String odd = palindromeSpreads(s, i, i);
        String even = palindromeSpreads(s, i, i + 1);
        if(odd.length() != 0){
           list.add(odd);
          }
         if(even.length() != 0 ){
            list.add(even);
          }
      }
      return list;
  }
  private static String palindromeSpreads(String s, int left, int right) {

    while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
      left--;
      right++;
    }
    return s.substring(left + 1, right);
  }
}
```

5. (Easy)Valid Palindrome II (leetcode 680)
```html
Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.
```
```java
public boolean palindrome(String s) {
  // idea is use recursive 
  int left = 0;
  int right = s.length() - 1;
  while(left < right&& s.charAt(left) == s.charAt(right)) {
    left++;
    right--;
  }
  if(left == right) return true;
  return (isPalindrome(s, left + 1, right) || isPalindrome(s, left, right+1);
}
private boolean isPalindrome(String s, int left, int right) {
  while(left < right) {
    if(s.charAt(left) != s.charAt(right)) {
      return false;
    }
  }
  return true;
}
```

6.(easy) Palindrome LinkedList leetcode(234)
```html
1. find middle point of LL.
2. reverse the second half 
3. compare first half with revesed second half, if it is not the same(value), break, return false
```
```java
public boolean palindromeInLL(ListNode head) {
   if(head == null) return true;
  //1. find middle point of LL
  ListNode walker = head;
  ListNode runner = head;
  while(runner.next != null && runner.next.next != null) {
    walker = walker.next;
    runner = runner.next.next;
  }
  
  //2. reverse LL 
  ListNode prev = null; 
  ListNode curr = walker.next;
  while(curr!= null) {
    ListNode temp = curr.next;
    curr.next = prev;
    prev = curr;
    curr = temp;
  }
  
  //3. comparing each node from first half and 2nd half
  ListNode head1 = head;
  ListNode head2 = prev;
  boolean equal = truel
  while(equal && head2 != null) {
    if(head1.val != head2.val) return false;
    head1 = head1.next;
    head2 = head2.next;
  }
  return equal

}
```








