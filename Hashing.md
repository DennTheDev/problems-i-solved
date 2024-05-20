
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>

## Hashing
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [First element occurring k times in an array](https://practice.geeksforgeeks.org/problems/first-come-first-serve1328/1) :

**Question** :

Given an array of n integers. The task is to find the first element that occurs k number of times. If no element occurs k times the print -1. The distribution of integer elements could be in any range.

**Intuition** :

Add all the elements and their counts in a HashMap. Return the **first element that has count equal to k**.

**Approach** :

Enter all elements in a HashMap. Then iterating through the array, if you find an element has count K return it. 

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution { 
    static int firstElement(int arr[], int n, int k) { 
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<n;i++){
            if(map.containsKey(arr[i])) {
                map.put(arr[i],map.get(arr[i])+1);
            }
            else map.put(arr[i],1);
        }
        for(int i=0;i<n;i++) {if(map.get(arr[i])==k) return arr[i];}
        return -1;
    }
}
```  
---  

2. #### [Find all pairs with a given sum](https://practice.geeksforgeeks.org/problems/find-all-pairs-whose-sum-is-x5808/1) :

**Question** :

Given two unsorted arrays A of size N and B of size M of distinct elements, the task is to find all pairs from both arrays whose sum is equal to X.

Note: All pairs should be printed in increasing order of u. For eg. for two pairs (u1,v1) and (u2,v2), if u1 < u2 then
(u1,v1) should be printed first else second.

**Intuition** :

Enter all elements of one array in and HashSet.  
Iterating through the second array check if required_sum-current_element in present in HashSet.

**Approach** :

Sort the first array.  
Add all the elements in a HashSet.  
Iterating through the second array check if Sum-current_element in HashSet and if so add to solution.  
Return the array of all pairs.

**Complexity** :  

- Time complexity: $O(n log n)$  

- Space complexity: $O(n)$ 

```java
class Solution {
    public pair[] allPairs( long A[], long B[], long N, long M, long X) {
        HashSet<Long> set=new HashSet<Long>();
        Arrays.sort(A);
        ArrayList<pair> sol=new ArrayList<pair>();
        for(int i=0;i<M;i++) set.add(B[i]);
        int c=0;
        for(int i=0;i<N;i++){
            if(set.contains(X-A[i])) sol.add(new pair(A[i],X-A[i]));
        } 
        pair[] ans=new pair[sol.size()];
        sol.toArray(ans);
        return ans;
    }
}
```  
---  
3. #### [Find common elements in three sorted arrays](https://practice.geeksforgeeks.org/problems/common-elements1132/1) :

**Question** :

Given three arrays sorted in increasing order. Find the elements that are common in all three arrays.
Note: You have to take care of the duplicates without using any additional Data Structure.

**Intuition** :

Eventhough this problem can be solved in $O(n1+n2+n3)$ time and $O(n1+n2+n3)$ space using two HashSets,  
we use an interation method to solve the problem in $O(n1+n2+n3)$ time and $O(1)$ space.

**Approach** :



**Complexity** :  

- Time complexity: $O(n1+n2+n3)$  

- Space complexity: $O(1)$ 

```java
class Solution
{
    ArrayList<Integer> commonElements(int A[], int B[], int C[], int n1, int n2, int n3) 
    {
        int p=0,q=0,r=0;
        ArrayList<Integer> list= new ArrayList<>();
        while(p<n1 && q< n2 && r< n3){
            if(p!=0 && A[p-1]==A[p]) {p++;continue;}
            while(B[q]<A[p] && q<n2-1)q++;
            while(C[r]<A[p] && r<n3-1)r++;
            if(A[p]==B[q]&& B[q]==C[r]) list.add(A[p]);
            p++;
        }
        return list;
    }
}
```  
---  
4. #### [Array Pair Sum Divisibility Problem](https://practice.geeksforgeeks.org/problems/array-pair-sum-divisibility-problem3257/1) :

**Question** :

Given an array of integers and a number k, write a function that returns true if the given array can be divided into pairs such that the sum of every pair is divisible by k.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution {
    public boolean canPair(int[] nums, int k) {
        if(nums.length%2!=0) return false;
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){map.put(((nums[i]%k)+k)%k,map.getOrDefault(((nums[i]%k)+k)%k,0)+1);}
        for(int i=0;i<nums.length;i++){
            int term=((nums[i]%k)+k)%k;
            if(2*term==k || term==0){
                if(map.get(term)%2!=0) return false;
            }
            else{
                if(map.get(term)!=map.get(k-term)) return false;
            }
        }
        return true;
    }
}
```  
---  
5. #### [Find whether an array is subset of another array](https://practice.geeksforgeeks.org/problems/array-subset-of-another-array2317/1) :

**Question** :

Given two arrays: arr1[0..m-1] and arr2[0..n-1]. Find whether arr2[] is a subset of arr1[] or not. Both arrays are not in sorted order. It may be assumed that elements in both arrays are distinct.

**Intuition** :

This question is similar to checking if two arrays are same or not. Just add all elements of the bigger array in a HashMap with their count and then by iterating the second array decrease the count of current element in the map. If count is zero or element is not in map then the second array is not a subarray.

**Approach** :

We initialise a map and **put all elements of bigger array and their counts in the map**.  
While traversing the second array **if element is not found in map or count is found to be zero, return false**.
**Decrease the count of current element**.
**Return true** after coming out of loop.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Compute {
    public String isSubset( long a1[], long a2[], long n, long m) {
        HashMap<Long,Integer> map=new HashMap<Long,Integer>();
        for(int i=0;i<n;i++)map.put(a1[i],map.getOrDefault(a1[i],0)+1);
        for(int i=0;i<m;i++){
            if((!map.containsKey(a2[i]))|| (map.containsKey(a2[i]) && map.get(a2[i])==0)){
                return "No";
            }
            map.put(a2[i],map.get(a2[i])-1);
        }
        return "Yes";
    }
}
```  
---  
6. #### [Find the element that appears once in sorted array](https://practice.geeksforgeeks.org/problems/element-appearing-once2552/1) :

**Question** :

Given a sorted array in which all elements appear twice (one after one) and one element appears only once. Find that element in O(log n) complexity.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(logn)$  

- Space complexity: $O(1)$ 

```java
class Sol{
    public static int search(int arr[], int N){
        int start=0,end=N-1,mid=0;
        while(start<end){
            mid=start+(end-start)/2;
            if((mid-start)%2!=0){
                if(arr[mid+1]==arr[mid]) end=mid-1;
                else start=mid+1;
            }
            else{
                if(arr[mid+1]==arr[mid]) start=mid;
                else end=mid;
            }
        }
        return arr[start];
    }
}
```  
--- 

7. #### [Longest Consecutive Subsequence](https://practice.geeksforgeeks.org/problems/longest-consecutive-subsequence2449/1) :

**Question** :

Given an array of integers, find the length of the longest sub-sequence such that elements in the subsequence are consecutive integers, the consecutive numbers can be in any order. 

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{   
    // arr[] : the input array
    // N : size of the array arr[]
    
    //Function to return length of longest subsequence of consecutive integers.
	static int findLongestConseqSubseq(int arr[], int N)
	
	{  
	   //if (N==0 || N==1) return 0;
	   int i,min=Integer.MAX_VALUE, max=Integer.MIN_VALUE,sol=0;
	   for(i=0;i<N;i++){
	       if(arr[i]<min)min=arr[i];
	       if(arr[i]>max)max=arr[i];
	   }
	   int [] table=new int[max-min+1];
	   for(i=0;i<N;i++){
	       table[arr[i]-min]=1;
	   }
	   i=1;
	   max= table[0]==1?1:0;
	   sol=max;
	   while(i<table.length){
	       if(table[i]==0) max=0;
	       else if(table[i]==1 && table[i-1]==1) max++;
	       else max=1;
	       if(max>sol)sol=max;
	       i++;
	   }
	   return sol;
	}
}
```  
---
8. #### [Count distinct elements in every window of size k](https://practice.geeksforgeeks.org/problems/count-distinct-elements-in-every-window/1) :

**Question** :

Given an array of integers and a number K. Find the count of distinct elements in every window of size K in the array.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    ArrayList<Integer> countDistinct(int A[], int n, int k)
    {
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        ArrayList<Integer> list=new ArrayList<Integer>();
        int count=0;
        for(int i=0;i<k;i++) {
            if(map.containsKey(A[i])) map.put(A[i],map.get(A[i])+1);
            else map.put(A[i],1);
        }
        list.add(map.size());
        for(int i=k;i<n;i++){
            if(map.get(A[i-k])>1) map.put(A[i-k],map.get(A[i-k])-1);
            else map.remove(A[i-k]);
            if(map.containsKey(A[i])) map.put(A[i],map.get(A[i])+1);
            else map.put(A[i],1);
            list.add(map.size());
        }
        return list;
        
    }
}
```  
--- 
9. #### [Zero Sum Subarrays](https://practice.geeksforgeeks.org/problems/zero-sum-subarrays1825/1) :

**Question** :

You are given an array arr[] of size n. Find the total count of sub-arrays having their sum equal to 0.

Examples: 

Input:  arr = [6, 3, -1, -3, 4, -2, 2, 4, 6, -12, -7]
Output:  
Subarray found from Index 2 to 4
Subarray found from Index 2 to 6          
Subarray found from Index 5 to 6
Subarray found from Index 6 to 9
Subarray found from Index 0 to 10

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(nlogn)$  

- Space complexity: $O(n)$ 

```java
class Solution{
    //Function to count subarrays with sum equal to 0.
    public static long findSubarray(long[] arr ,int n) 
    {   
        long sol=0;
        HashMap<Long,Integer> map=new HashMap<Long,Integer>();
        int i;
        for(i=1;i<n;i++) arr[i]+=arr[i-1];
        map.put(new Long(0),1);
        for(i=0;i<n;i++){
            if(map.containsKey(arr[i])){
                sol+=map.get(arr[i]);
                map.put(arr[i],map.get(arr[i])+1);
            }
            else map.put(arr[i],1);
        }
        return sol;
    }
}
```  
---  
</div>
