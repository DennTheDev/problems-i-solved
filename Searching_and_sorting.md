

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>

## Searching and Sorting
### Approaches:
* **Binary Search** :  
When array is sorted, compare the middle element with required element  
if find the element we return it.  
Else we move to the appropriate half of the array and repeat the process to zero-in on the required element.  
After finding the middle element how we choose to procced and which half to choose  
makes this search more **powerful** than just searching for an element.  
We can search for pivot points in rotated arrays,etc.

* **Mergesort** :  
This is a divide and conquer algorithm where we divide arrays and in the joining step we merge them in sorted order.  
After the algorithms bottoms out and them finishes merging all sub-arrays, the entire array is sorted.  
The merge function of this method can be used in clever ways to make the solution more space efficient.[See](#merge-sorted-array)  


### Problems:
1. #### [Binary Search](https://practice.geeksforgeeks.org/problems/binary-search-1587115620/1) :

**Question** :

Given a sorted array of size N and an integer K, find the position at which K is present in the array using binary search.

**Intuition** :

Classic Binary search algorithm. If the array is **sorted**, we travel to the middle of the array  
**if we find the element we return the index**,  
if the **required element is greater than middle element we search for it in the right half**,  
if the **required element is smaller we look for it in the left half**.

**Approach** :

We define a **start** and **end** pointer and while start<=end,  
We calculate the middle element **m** and **check if it's the required element, and if so we return it**.  
Else **if required element is smaller than middle element, then end = m-1**,  
**else start = m+1**.

**Complexity** :  

- Time complexity: $O(log n)$  

- Space complexity: $O(log n)$ if recursively else $O(1)$ 

```java
class Solution {
    int binarysearch(int arr[], int n, int k) {
        int m=0,start=0,end=n-1;
        while(start<=end){
            m=start+(end-start)/2;
            if(arr[m]==k) return m;
            else if(arr[m]<k) start=m+1;
            else end=m-1;
        }
        return -1;
    }
}
```  
---  
2. #### [Merge Sort](https://practice.geeksforgeeks.org/problems/merge-sort/1) :

**Question** :

Given an array arr[], its starting position l and its ending position r. Sort the array using merge sort algorithm.

**Intuition** :

Implementation of mergesort algorithm.

**Approach** :

This is a divide and conquer algorithm where we divide arrays and in the joining step we merge them in sorted order.  
After the algorithms bottoms out and them finishes merging all sub-arrays, the entire array is sorted. 

**Complexity** :  

- Time complexity: $O(n log n )$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    void merge(int arr[], int l, int m, int r)
    {
        int n1=m-l+1, n2=r-m;
        int[] L= new int [n1],R= new int [n2];
        for(int i=0;i<n1;i++) L[i]= arr[i+l];
        for(int i=0;i<n2;i++) R[i]= arr[i+m+1];
        int i=l,p=0,q=0;
        while(i<=r){
            while(p<n1 && q<n2){
                if(L[p]<=R[q]){arr[i]=L[p++];}
                else{arr[i]=R[q++];}
                i++;
            }
            while(p<n1) {arr[i]=L[p++];i++;}
            while(q<n2) {arr[i]=R[q++];i++;}
        }
    }
    void mergeSort(int arr[], int l, int r)
    {
        if(r==l) return ;
        int m= l+(r-l)/2;
        mergeSort(arr,l,m);
        mergeSort(arr,m+1,r);
        merge(arr,l,m,r);
    }
}
```  
---  

3. #### [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array) :

**Question** :

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

**Intuition** :

I used another array to copy the elements of first array and then used classic mergesort merge function.  
But the better way was to **apply mergesort merge function to put elements in reverse order instead of increasing**.

**Approach** :

Starting form the end of both arrays(**p1=m-1 for array1 and p2=n-1 for array2**),  
we add **greater of nums1[p1] and num2[p2] in nums1[i]**, and decrease **p1 or p2 respectively** and **decrease i** as well.  
If **p1 becomes less than zero then we add the rest of nums2 in nums1**.  
If **p2 becomes zero then array is already sorted**.

**Complexity** :  

- Time complexity: $O(n+m)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int p1=m-1,p2=n-1,i=m+n-1;
        while(p2>=0){
            if(p1>=0 && nums1[p1]>nums2[p2]) {nums1[i]=nums1[p1];p1--;}
            else {nums1[i]=nums2[p2];p2--;}
            i--;
        }
    }
}
```  
---  
4. #### [Search an element in a sorted and rotated Array](https://practice.geeksforgeeks.org/problems/search-in-a-rotated-array4618/1) :

**Question** :

Given a sorted and rotated array arr[] of size N and a key, the task is to find the key in the array.

**Intuition** :

Find the partition where the array is rotated using **Binary Search**.
Then check in which half the key may lie and then do a **Binary Search** in that part of array. 

**Approach** :

Define a **Binary Search function which searches for the rotation partition**.  
This is just the **modified version of Binary Search that checks if arr[mid+1] < arr[mid] instead of arr[mid]==key**.
After finding the **partition,i.e. i**, **check if key lies in [arr[ 0 ], arr[ mid ]], both inclusive**, and **if it is Binary Search key in that subarray using Array.binarySearch(arr,0,i+1,key).**
**Else Binary Search the other sub array by Array.binarySearch(arr,i+1,arr.length,key)**.
If element **if found return the index, else return -1**.

**Complexity** :  

- Time complexity: $O(logn)$  

- Space complexity: $O(1)$ 

```java
class Solution
{
    int partition(int[] arr){
        int n=arr.length-1;
        int index=n-1;
        int start=0,end=n-1,mid=0;
        if(arr[start]>arr[end]){
            while(start<=end){
                mid=(start+end)/2;
                if (arr[mid+1]<arr[mid]){return mid;}
                if(arr[mid]<arr[start]) end=mid;
                else start=mid+1;
            }
        }
        return index;
    }
    int search(int A[], int l, int h, int key)
    {
        int i=partition(A);
        int ans=0;
        if(key>=A[0] && key<=A[i]) ans=Arrays.binarySearch(A,0,i+1,key);
        else ans= Arrays.binarySearch(A,i+1,A.length,key);
        return ans<0? -1: ans;
    }
}
```  
---  
5. #### [Sort elements by frequency](https://practice.geeksforgeeks.org/problems/sorting-elements-of-an-array-by-frequency/0) :

**Question** :

Given an array A[] of integers, sort the array according to frequency of elements. That is elements that have higher frequency come first. If frequencies of two elements are same, then smaller number comes first.

**Intuition** :

We store 

**Approach** :



**Complexity** :  

- Time complexity: $O(nlogn )$  

- Space complexity: $O(n)$ 

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {
	public static void main (String[] args) {
		Scanner sc=new Scanner(System.in);
		int n=sc.nextInt();
		for(int i=0;i<n;i++){
		    int N=sc.nextInt();
		    ArrayList<Integer> arr=new ArrayList<Integer>();
		    int k=0,c=0;
		    HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
		    for(int j=0;j<N;j++){
		        k=sc.nextInt();
		        if(map.containsKey(k)) map.put(k,map.get(k)+1);
		        else{
		            arr.add(k);
		            map.put(k,1);
		        }
		    }
		    Collections.sort(arr, new Comparator<Integer>(){
		        @Override
		        public int compare(Integer a,Integer b){
		            int aa=map.get(a);
		            int bb=map.get(b);
		            if(aa==bb) return a.compareTo(b);
		            return map.get(a)>map.get(b)?-1:1;
		        }
		        
		    });

	        for(int x=0;x<arr.size();x++){
	            for(int y=0;y<map.get(arr.get(x));y++) System.out.print(arr.get(x)+" ");
	        }
	        System.out.println();
		}
	}
}
```  
--- 
</div>
