## KMP
```html
   －	Example: ABCDABD
   －　"A"的前缀和后缀都为空集，共有元素的长度为0；

　　－　"AB"的前缀为[A]，后缀为[B]，共有元素的长度为0；

　　－　"ABC"的前缀为[A, AB]，后缀为[BC, C]，共有元素的长度0；

　　－　"ABCD"的前缀为[A, AB, ABC]，后缀为[BCD, CD, D]，共有元素的长度为0；

　　－　"ABCDA"的前缀为[A, AB, ABC, ABCD]，后缀为[BCDA, CDA, DA, A]，共有元素为"A"，长度为1；

　　－　"ABCDAB"的前缀为[A, AB, ABC, ABCD, ABCDA]，后缀为[BCDAB, CDAB, DAB, AB, B]，共有元素为"AB"，长度为2；

　　－　"ABCDABD"的前缀为[A, AB, ABC, ABCD, ABCDA, ABCDAB]，后缀为[BCDABD, CDABD, DABD, ABD, BD, D]，共有元素的长度为0。

Longest Common prefix and sufix = 'AB'

pattern.   : A B C D A B D
commonIndex: 0 0 0 0 1 2 0

```

```java
class KMP {
	public static void getNext(String pattern, int[] longestCommonPrefixSuffix) {

		//pattern: abcabcabd 
		int j = 0;
		int k = -1;
		int patternLength = pattern.length();
		longestCommonPrefixSuffix[0] = -1;

		while( j < patternLength - 1) {
			if(k == -1 || pattern.charAt(k) == pattern.charAt(j)) {
				j++;
				k++;
				longestCommonPrefixSuffix[j] = k; // [1] = 0, [2] = 0, [3] = 0, [4] = 1 [5] = 2
				System.out.println(pattern.charAt(k) + " " + pattern.charAt(j));
				System.out.println("longestCommonPrefixSuffix[" +  j + "] = " + k);
			}else{
				k = longestCommonPrefixSuffix[k]; //next[0] = -1;
				System.out.println("longestCommonPrefixSuffix[" +  k + " ] = " + k);
			}

		}
	}
	public static int kmp(String s, String pattern) {
		int i = 0, j = 0;
		int slen = s.length();
		int plen = pattern.length();
		int[] longestCommonPrefixSuffix = new int[plen];

		getNext(pattern, longestCommonPrefixSuffix);

		System.out.print("longestCommonPrefixSuffix: ");
		for(int k: longestCommonPrefixSuffix) {
			System.out.print( k + " ");
		}
		System.out.println();
		while(i < slen && j < plen) {
			if(s.charAt(i) == pattern.charAt(j)) {
				i++;
				j++;
			}
			else {
				if(longestCommonPrefixSuffix[j] == -1) { // in the beginning
					//System.out.println("next[j]  " + next[j] );
					i++;
					j = 0;
				}
				else {
					System.out.println("j  " + j );
					System.out.println("longestCommonPrefixSuffix[j]  " + longestCommonPrefixSuffix[j] );
					j = longestCommonPrefixSuffix[j];
				}
			}
			if(j == plen) { // find the pattern 
				return i - j;
			}
		}
		return -1;
	}
	public static void main(String[] args) {
		KMP kmp = new KMP();
		String str = "fffffabcabcabcabcabdfffff";
		String pattern = "abcabcabd";
		System.out.println(str);
		
		int num = kmp(str, pattern);
		for(int i = 0; i < num; i++) {
			System.out.print(" ");
		}
		System.out.println(pattern);
		
	}
}
```
