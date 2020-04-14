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