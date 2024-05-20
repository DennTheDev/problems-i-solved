

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>
  
## Strings
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Find the first repeated character in a string](https://practice.geeksforgeeks.org/problems/find-first-repeated-character4108/1) :

**Question** :

Given a string, find the first repeated character in it. We need to find the character that occurs more than once and whose index of second occurrence is smallest.

**Intuition** :

Use a character array to keep track of which characters have been seen. If we find a previously seen character, return the character.  
Else return -1.

**Approach** :

Initialise the **character array** and while iterating the String, **check if current character has been visited**. **If yes return the character**.  
**Else put 1 in the index of the current character in the character array**.  
**If no character repeated, return -1**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution 
{ 
    String firstRepChar(String s) 
    { 
        int[] arr=new int[256];
        for(int i=0;i<s.length();i++){
            if(arr[(int)s.charAt(i)]==1) return ""+s.charAt(i);
            arr[(int)s.charAt(i)]=1;
        }
        return "-1";
    }
} 
```  
---  
2. #### [Check if a string can be obtained by rotating another string 2 places](https://practice.geeksforgeeks.org/problems/check-if-string-is-rotated-by-two-places-1587115620/1) :

**Question** :

Given two strings, the task is to find if a string can be obtained by rotating another string by two places. 

**Intuition** :

Check the **rotation both ways by 2 places** and **if either one satisfies return true, else false**.

**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution
{
    public static boolean isRotated(String str1, String str2)
    {
        boolean left=true, right=true;
        int n=str1.length();
        for(int i=0;i<str1.length();i++){
            if(str1.charAt(i)!=str2.charAt((i+2)%n)){
                right=false;
                break;
            }
        }
        for(int i=0;i<str2.length();i++){
            if(str1.charAt((i+2)%n)!=str2.charAt(i)){
                left=false;
                break;
            }
        }
        return left||right;
    }
    
}
```  
---  
3. #### [Remove duplicates from a given string](https://practice.geeksforgeeks.org/problems/remove-duplicates/0) :

**Question** :

Given a string S, the task is to remove all the duplicates in the given string.

**Intuition** :

Use a **LoopTable(Array)** to keep track of previously seen characters. Only add unique characters to solution.

**Approach** :

Initialise **an array of length 256**.  
Iterating through the array, **check if Array[character] is 1**,i.e., **if you have seen the character before**.  
**If its not 1, set Array[character] as 1 and add the character to the solution**. **Else, keep iterating**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    String removeDups(String S) {
        StringBuilder sb=new StringBuilder();
        //Lookup table using an array can also be used instead of a hashmap
        HashSet<Character> set=new HashSet<Character>();
        for(int i=0;i<S.length();i++){
            if(!set.contains(S.charAt(i))){sb.append(S.charAt(i));set.add(S.charAt(i));}
        }
        return sb.toString();
    }
}
```  
---  
4. #### [Longest Common Prefix](https://practice.geeksforgeeks.org/problems/longest-common-prefix-in-an-array5129/1) :

**Question** :

Given a array of N strings, find the longest common prefix among all strings present in the array.

**Intuition** :

We keep comparing characters at some index i for all string, where i varies from 0 to length of the smallest string in the array and wherever the characters differ we break and return the substring till which the characters match.

**Approach** :

First we find the length of the string with the minimum length and set min to that value.
We initialise i as 0.
For i varying from 0 to min, if character at i of a string differs from others, we break and return the substring till i.

**Complexity** :  

- Time complexity: $O(N*max(|arri|))$  

- Space complexity: $O(1)$ 

```java
class Solution{
    String longestCommonPrefix(String arr[], int n){
        int c=0;
        for(int i=0;i<arr[0].length();i++){
            for(int j=1;j<n;j++){
                if(i>=arr[j].length() || arr[0].charAt(i)!=arr[j].charAt(i)) 
                    return c==0?"-1":arr[0].substring(0,c);
            }
            c++;
        }
        return c==0?"-1":arr[0].substring(0,c);
    }
}
```  
---  
5. #### [Minimum indexed character](https://practice.geeksforgeeks.org/problems/minimum-indexed-character-1587115620/1) :

**Question** :

Given a string str and another string patt. Find the character in patt that is present at the minimum index in str. If no character of patt is present in str then print ‘No character present’.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution{
    public static int minIndexChar(String str, String patt){
        HashSet<Character> set=new HashSet<Character>();
        int min=Integer.MAX_VALUE;
        for(int i=0;i<patt.length();i++) set.add(patt.charAt(i));
        for(int i=0;i<str.length();i++) if(set.contains(str.charAt(i)) && i<min){ min=i; break;}
        return min==Integer.MAX_VALUE?-1:min;
    }
}
```  
--- 
</div>
