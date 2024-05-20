

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>

## Dynamic Programming
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Edit Distance](https://leetcode.com/problems/edit-distance/) :

**Question** :

Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

* Insert a character
* Delete a character
* Replace a character

**Intuition** :

Like all DP problems, the way to approach the problem was to develop a bruteforce solution and proceed from there.
We outline a bruteforce method, where we compare the characters of string1 at i and string2 at j.

***Bruteforce Approach***:
If character at i is equal to character at j, then we just decrement both pointers and calculate the solution for i-1 and j-1.
Since, both characters are same no opertions are required.

Else we find the minimum of insert, update or delete operations for current subproblem return it.

For the base case, if either of strings being used becomes empty we return value of other pointer+1 since thats how many operations it would take to make both the string equal at the current condition.

* **Insert**: Imagine we put string2[j] infront of string1[i]. Insertion takes 1 operation and we move to compare the rest of string2 with the current string1 and hence calculate the solution **for i and j-1**. **Total operations is 1+ recurive call for i,j-1.**
* **Delete**: Imagine we just removed the character at string1[i] and solve the rest of string1 and current string2. We will have to calculate the solution **for i-1 and j**. **Total operations is 1+ recurive call for i-1,j.**
* **Update**: Imagine we update the value of character at string1[i] as the character of string2[j]. Then we move on to calculate the solution of subproblem **for i-1 and j-1**. **Total operations is 1+ recurive call for i-1,j-1.**

**Approach** :

Leveraging the bruteforce method, we optimise it using DP since optimal substructures and overlapping subcases exist.
We make a DP table of m+1 and n+1 dimension and start filling it using the logic from recursive approach.
If the character at string1[j-1] is equal to string2[i-1] we fill the current cell as arr[i-1][j-1].
Else we fill it as min(arr[i-1][j-1],arr[i-1,j],arr[i,j-1]).

This table can be furthur space optimized. Since only two rows are being used at any given time, we only save the data of required rows in 2 1-D array and keep updating them.

**Complexity** :  

- Time complexity: $O(m*n)$  

- Space complexity: $O(m)$ 

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m=word1.length(),n=word2.length();
        Character p,q;
        int[] curr=new int[m+1];
        int[] prev=new int[m+1];
        for(int i=0;i<=m;i++) prev[i]=i;
        for(int i=1;i<=n;i++){
            curr[0]=i;
            for(int j=1;j<=m;j++){
                p=word1.charAt(j-1);
                q=word2.charAt(i-1);
                if(p==q){
                    curr[j]=prev[j-1];
                }
                else{
                    curr[j]=1+Math.min(prev[j-1],Math.min(prev[j],curr[j-1]));
                }
            }
            prev=curr.clone();
        }
        return prev[m];
    }
}
```  
---  

2. #### [Longest Common Substring](https://practice.geeksforgeeks.org/problems/longest-common-substring1452/1) :

**Question** :

Given two strings. The task is to find the length of the longest common substring.

**Intuition** :

***Bruteforce Approach:***
In this problem, the idea of the **bruteforce approach** is that, we go compare the ith character of string1 and jth character of string2 and whilst both match, we keep decreasing i and j and increasing a count. We compare the count now, subcase of leaving a character from string1 and another subcase of leaving character from string2. We return max of these values. 

For the base case, if either string turn up empty we return 0 since there can be no common substring.

**Approach** :

We can optimze the solution using a 2D array that stores the values of sub-problems. While filling the table **if ith character and jth character match**, then the current cell will be filled with value **1+arr[i-1][j-1]**. **Else fill it with zero**. Compare the current array entry to a max variable and if the entry is greater than max, update the max variable. At last we return the max variable.

**Complexity** :  

- Time complexity: $O(m*n)$  

- Space complexity: $O(m*n)$ 

```java
class Solution{
    int longestCommonSubstr(String S1, String S2, int n, int m){
        int max=0;
        int [][] arr= new int[n+1][m+1];
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n;j++){
                if(S1.charAt(j-1)==S2.charAt(i-1)) {
                    arr[j][i]=1+arr[j-1][i-1];
                    if(arr[j][i]>max) max=arr[j][i];
                }
            }
        }
        return max;
    }
}
```  
---  

3. #### [Longest Common Subsequence](https://practice.geeksforgeeks.org/problems/longest-common-subsequence-1587115620/1) :

**Question** :

Given two sequences, find the length of the longest subsequence present in both of them. A subsequence is a sequence that appears in the same relative order but is not necessarily contiguous. For example, “abc”, “abg”, “bdf”, “aeg”, ‘”acefg”, .. etc are subsequences of “abcdefg”. 

**Intuition** :

***Bruteforce Approach:***
While comparing string1 at i and string2 at j, **if the characters match then return 1+subproblem(i-1,j-1)**, else return **max(subproblem(i-1,j),subproblem(i,j-1))**. 
If the **i==-1 or j==-1 we return 0**.

**Approach** :

The logic from the bruteforce approach is implemented using an array and since we use only two rows at any given time, we can furthur optimize the space into 2 1D arrays.

**Complexity** :  

- Time complexity: $O(x*y)$  

- Space complexity: $O(x)$ 

```java
class Solution
{
    //Function to find the length of longest common subsequence in two strings.
    static int lcs(int x, int y, String s1, String s2)
    {
        int[] prev=new int[x+1];
        int[] curr=new int[x+1];
        for(int i=1;i<=y;i++){
            for(int j=1;j<=x;j++){
                if(s1.charAt(j-1)==s2.charAt(i-1)) curr[j]=prev[j-1]+1;
                else curr[j]=Math.max(curr[j-1],prev[j]);
            }
            prev=curr.clone();
        }
        return prev[x];
    }
    
}
```  
---  

</div>
