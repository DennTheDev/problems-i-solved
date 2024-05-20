

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">

<div>

<img src="./Illustrations/sde.gif"/>

## Bit Magic
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Position of rightmost set bit](https://practice.geeksforgeeks.org/problems/find-first-set-bit-1587115620/1) :

**Question** :

Write a one-line function to return the position of the first 1 from right to left, in the binary representation of an Integer. 

**Intuition** :

Use 2s complement to find the set bit;

**Approach** :

(int)Math.log10(n & -n)/Math.log10(2) returns the index of first set bit.

**Complexity** :  

- Time complexity: $O(log2(n))$  

- Space complexity: $O(1)$ 

```java
class Solution
{
    public static int getFirstSetBit(int n){
        if(n==0) return 0;    
        return (int)((Math.log10(n & -n)) / Math.log10(2))
            + 1;
            
    }
}
```  
---  
2. #### [Check whether K-th bit is set or not](https://practice.geeksforgeeks.org/problems/check-whether-k-th-bit-is-set-or-not-1587115620/1) :

**Question** :

Given a number N and a bit number K, check if the Kth bit of N is set or not. A bit is called set if it is 1. 

**Intuition** :

Do an bitwise-AND operation of the number and 1 left shifted k times and check if its not equal to zero.

**Approach** :

Check if (n &( 1<< k) ) not equal to zero.

**Complexity** :  

- Time complexity: $O(1)$  

- Space complexity: $O(1)$ 

```java
class CheckBit
{
    // Function to check if Kth bit is set or not.
    static boolean checkKthBit(int n, int k)
    {
        return (n &(1<<k) ) !=0;
    }
    
}
```  
---  
3. #### [Set kth bit](https://practice.geeksforgeeks.org/problems/set-kth-bit/0) :

**Question** :

Given a number N and a value K. From the right, set the Kth bit in the binary representation of N. The position of Least Significant Bit(or last bit) is 0, the second last bit is 1 and so on.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(1)$  

- Space complexity: $O(1)$ 

```java
class Solution{
    static int setKthBit(int N,int K){
        return (N & (1<<K)) >0 ? N : N^(1<<K);
    }
}
```  
---  
4. #### [Power of 2](https://practice.geeksforgeeks.org/problems/power-of-2-1587115620/1) :

**Question** :

Given a positive integer n, write a function to find if it is a power of 2 or not

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(1)$  

- Space complexity: $O(1)$ 

```java
class Solution{
    
    // Function to check if given number n is a power of two.
    public static boolean isPowerofTwo(long n){
        return (n!=0) && ((n & (n-1))==0);
    }
    
}
```  
---  

</div>
