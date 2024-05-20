

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>

[Review Notes](https://algs4.cs.princeton.edu/10fundamentals/)

## Array
### Approaches:
* **Iteration (Normal and reverse)** :  
E.g.:  
    * Leaders in array (reverse iteration)  
* **Two pointer method** :  
Set a pointer at the start of the array and at the end.  
E.g.:  
    * Find pivot element where left_sum==right_sum when all elements are positive
* **Three pointer method** :  
Set a pointer at the start of the array, one at the end and another one for iteration.  
Its an extension of two-pointer method.  
E.g.:  
    * Dutch National Flag Problem  
    * Reverse array in groups
* **Prefix sum method** :  
Find sum of all array elements up to that point.   
E.g.:  
    * Find pivot elements where left sum==right sum  
* **Using HashSet or HashMap with array** :  
Using a HashSet to check if a number is present in an array or not,  
or count of characters in HashMap,etc.  
E.g.:
    * Swapping pairs making sum equal(HashSet)
    * Check if two arrays are equal or not
* **Sliding window approach** :  
We take two pointers, and the elements between the pointers is called the window.  
By increasing the end and start of the window, the window slides and  
is useful to find subarray satisfying some condition.  
E.g.:
    * Subarray with given sum

### Problems:  
1. #### [Leaders in an array](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side) :

**Question** :

Given an array arr, replace every element in that array with the greatest element among the elements to its right, and replace the last element with -1.

After doing so, return the array.

**Intuition** :  
Thought of iteration from back to front of array while saving the max element upto that point.

**Approach** :

**Iterate from back to front** of the array while **saving the max element upto that point**.  
Last element will always be leader since no elements are present to its right.  
Put the last element in a solution array and keep updating the max value as you traverse   
from the back to front and whenever you encounter an element greater than max,  
add that element to solution array and update max variable.  
Finally return the solution array by reversing it.  
Note that **if there are no elements or one element in the array return the array itself**.  
In the leetcode question, **it was specified to put -1 instead of last element**  
and therefore instead of returning the array I returned an array containing -1  
and in the array of leaders there is -1 instead of last element.  

**Complexity** :

- Time complexity: $O(n)$

- Space complexity: $O(1)$  

```java
class Solution {
    public int[] replaceElements(int[] arr) {
        int max=arr[arr.length-1],temp=0;
        arr[arr.length-1]=-1;
        for(int i=arr.length-2;i>=0;i--){
            temp=arr[i];
            arr[i]=max;
            if(temp>max) max=temp;
        }
        return arr;
    }
}
```  
---  


2. #### [Equilibrium point / Find pivot index](https://leetcode.com/problems/find-pivot-index) :

**Question** :

Given an array of integers nums, calculate the pivot index of this array.

The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.

If the index is on the left edge of the array, then the left sum is 0 because there are no elements to the left. This also applies to the right edge of the array.

Return the leftmost pivot index. If no such index exists, return -1.

**Intuition** :

At first i though of using the two pointer method and it worked fine when all elements are positive  
but I ran cases when negative elements came into the picture and the code became complicated.  
The **prefix sum method** provided an optimal solution.

**Approach** :

Firstly we find **the sum off all elements** in the array.  
Next we traverse the array, and check where **leftsum==rightsum**.  
Now we can **calculate left sum as we traverse**, and **right sum is  
sum-leftsum-current_element** and **check if both are equal**.  


**Complexity** : 
- Time complexity: $O(n)$


- Space complexity: $O(1)$


```java
class Solution {
    public int pivotIndex(int[] nums) {
        int sum=0,leftsum=0;
        for ( int x: nums) sum+=x;
        for ( int i=0 ; i<nums.length ; i++){
            if(leftsum==sum-leftsum-nums[i]) return i;
            leftsum+=nums[i];
        }
        return -1;
    }
}
```
---

3. #### [Sort Colors](https://leetcode.com/problems/sort-colors) :

**Question** :

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Intuition** :

Traverse through the array while keeping in track where to put 0 or 2 if I encounter it.

**Approach** :

Take 3 pointers **one for iteration(k)**, and **other two denoting where 0(i) or 2(j) will be put if found**.  
This question uses **three-pointer method** and we proceed as follows.  
If we encounter a zero, we swap it with element at position i and i++ and k++.  
If we encounter a one, we just k++.  
If we encounter a two, we swap with element at position j and j--.  
The reason we dont increase the k pointer after swapping with j  
is that we dont know what the value of element at j pointer is.  
But in the case of i pointer we increase both values because we know  
we will be swapping the current element with itself or a one.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    public void sortColors(int[] nums) {
        int i=0, j=nums.length-1,k=0;
        while(k<=j){
            if (nums[k]==1) k++;
            else if(nums[k]==0){
                nums[k]=nums[i];
                nums[i]=0;
                i++;
                k++;
            }
            else{
                nums[k]=nums[j];
                nums[j]=2;
                j--;
            }
        }
    }
}
```  
---  

4. #### [Reverse array in groups](https://practice.geeksforgeeks.org/problems/reverse-array-in-groups/0) :

**Question** :

Given an array arr[] and an integer K, the task is to reverse every subarray formed by consecutive K elements.

**Intuition** :

Take a pointer at start of the list and reverse  
elements k at a time using swapping.

**Approach** :

Take two pointers start and end.  
Iterate through the list, increasing the iterator index by k.  
assign **start as the interator index** and **end as min((n-1),index+k-1))**.  
**In each iteration swap elements of start and end while start < end  
and start++ and end--**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    //Function to reverse every sub-array group of size k.
    void reverseInGroups(ArrayList<Integer> arr, int n, int k) {
        int start=0,end=0;
        for(int i=0;i<n;i+=k){
            start=i;end=Math.min(n-1,i+k-1);
            while(start<end){
                Collections.swap(arr,start++,end--);
            }
        }
    }
}
```  
---  

5. #### [Convert Array into Zig-Zag fashion](https://practice.geeksforgeeks.org/problems/convert-array-into-zig-zag-fashion/0) :

**Question** :

Given an array arr of distinct elements of size N, the task is to rearrange the elements of the array in a zig-zag fashion so that the converted array should be in the below form: 

arr[0] < arr[1]  > arr[2] < arr[3] > arr[4] < . . . . arr[n-2] < arr[n-1] > arr[n]. 

**Intuition** :

Since the array must follow arr[0]< arr[1] > arr[2] < .... and so on  
We can just interate the array and swap where the condition doesn't satisfy.

**Approach** :

We interate though the array **from 1 to n-1** and  
on **even indices if element > previous index element**  
and **on odd indices if element < previous element**  
we swap.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution{
    public void zigZag(int a[], int n){
        for(int i=1;i<n;i++){
            if((i%2!=0 && a[i]<a[i-1]) || (i%2==0 && (a[i]>a[i-1]))){
                a[i]=a[i]+a[i-1];
                a[i-1]=a[i]-a[i-1];
                a[i]=a[i]-a[i-1];
            }
        } 
    }
}
```  
---  

6. #### [Rearrange array alternatively](https://practice.geeksforgeeks.org/problems/-rearrange-array-alternately/0/) :

**Question** :

Given a sorted array of positive integers. Your task is to rearrange the array elements alternatively i.e first element should be max value, second should be min value, third should be second max, fourth should be second min and so on.
Note: Modify the original array itself. Do it without using any extra space. You do not have to return anything.

**Intuition** :

This question was quite complicated and one of a kind since I had never encountered   
such question before. I wasn't sure how to do it without using extra space  
(i.e. traversing from either side and adding max and min elements to an array alternatively). 

**Approach** :

Okay.  
We transform each element of the array as such:  
**element+= (desired_element % max) * max**
where max is maximum element in the array +1 and  
desired element is min or max element depending on position.  
So, the most efficient approach deals with the problem by  
**saving current element in the remainder part** and  
**desired element in the quotient part**.  


**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution{
    public static void rearrange(long arr[], int n){
        long max=arr[n-1]+1;
        int start=0,end=n-1;
        for(int i=0;i<n;i++){
            if (i%2==0) arr[i]+=(arr[end--]%max)*max;
            else arr[i]+= (arr[start++]%max)*max;
        }
        for(int i=0;i<n;i++) arr[i]/=max;
    }
}
```  
---  

7. #### [Missing number in array](https://leetcode.com/problems/missing-number) :

**Question** :

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

**Intuition** :

To find the number that is missing from a range we can first find the sum of all numbers in that  
range and then subtract the sum of all elements from the given array.  
Alternatively another solution is to xor all the elements in the range and xor all elements  
in the given array and then xor both values.

**Approach** :

Find **xor of all the elements in range [0,n]** both inclusive (**results in m**) and then find  
**xor of all the elements in the given array (results in l)** and **return m^l**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    public int missingNumber(int[] nums) {
        int n=nums.length,m=0,l=0;
        for(int i=1;i<=n;i++) {
            m^=i;
            l^=nums[i-1];
        }
        return m^l;
    }
}
```  
---  

8. #### [K-th element of two sorted Arrays](https://practice.geeksforgeeks.org/problems/k-th-element-of-two-sorted-array/0) :

Note: This is the $O(k)$ solution. Better solution will be updated later.

**Question** :

Given two sorted arrays of size m and n respectively, you are tasked with finding the element that would be at the k’th position of the final sorted array.

**Intuition** :

After reading the question, merge funnction of merge sort came to mind immediately.

**Approach** :

This approach involves taking **2 pointers for traversing both the given arrays**.  
We initalise both pointers to zero and compare current element in both arrays.  
Whichever **element is smaller we increase that pointer** and **update a counter** and **save   
the last touched element in a variable**.  
**If one of the arrays finish we traverse the rest of other array**.  
**We return the last touched element when counter equalizes with k**.

**Complexity** :  

- Time complexity: $O(k)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    public long kthElement( int arr1[], int arr2[], int n, int m, int k) {
        int i=0,j=0,c=0;
        long sol=0;
        while(i<n && j<m){
            if (arr1[i]<arr2[j]){sol=arr1[i++];}
            else {sol=arr2[j++];}
            c++;
            if(k==c) return sol;
        }
        while(i<n && c!=k) {sol=arr1[i++]; c++; }
        while(j<m && c!=k) {sol=arr2[j++]; c++; }
        return sol;
    }
}
```  
---  

9. #### [Check if two arrays are equal or not](https://practice.geeksforgeeks.org/problems/check-if-two-arrays-are-equal-or-not/0) :

**Question** :

Given two arrays A and B of equal size N, the task is to find if given arrays are equal or not. Two arrays are said to be equal if both of them contain same set of elements, arrangements (or permutation) of elements may be different though.
Note : If there are repetitions, then counts of repeated elements must also be same for two array to be equal.

**Intuition** :

Initial intuition was to check if elements present in both and their counts in both arrays are same or not.  
Found a better approach to solve using HashMap.

**Approach** :

**Traverse the first array and save the counts of all elements in a HashMap**.  
Now **traverse the second array** and **reduce the count of elements that you encounter**.  
If you find **elements not in the HashMap** or whose **count is already 0**, **return False**.  
Else, **return True**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution{
    //Function to check if two arrays are equal or not.
    public static boolean check(long A[],long B[],int N)
    {
        HashMap<Long,Integer> map= new HashMap<Long,Integer>();
        for(int i=0;i<N;i++) {
            if(map.containsKey(A[i])) map.put(A[i],map.get(A[i])+1);
            else map.put(A[i],1);
        }
        for(int i=0;i<N;i++){
            if(!map.containsKey(B[i]) || map.get(B[i])==0) return false;
            map.put(B[i],map.get(B[i])-1);
        }
        return true;
    }
}
```  
---  

10. #### [Kadane’s Algorithm](https://leetcode.com/problems/maximum-subarray/) :

**Question** :

Given an integer array nums, find the subarray with the largest contigous sum, and return its sum.

**Intuition** :

Algorithm to find maximum contigous sub-array.

**Approach** :

We traverse the array and update a **current_maximum with Max(current_maximum+current_element,current_element)**.  
Whenever **current_maximum > max variable, update max variable**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    public long maxSubArray(int[] nums) {
        long sum=nums[0],max=nums[0];
        for(int i=1;i<nums.length;i++){
            sum=Math.max(sum+nums[i],nums[i]);
            if(sum>max) max=sum;
        }
        return max;
    }
}
```  
---  

11. #### [Save Your Life](https://practice.geeksforgeeks.org/problems/save-your-life4601/1) :

Note: Its an implementation of Kadane's Algorithm.

**Question** :

Given a string w, integer array b,  character array x and an integer n. n is the size of array b and array x. Find a substring which has the sum of the ASCII values of its every character, as maximum. ASCII values of some characters are redefined.
Note: Uppercase & lowercase both will be present in the string w. Array b and Array x contain corresponding redefined ASCII values. For each i, b[i] contain redefined ASCII value of character x[i].

**Intuition** :

Similar to Kadane's algorithm but instead of an array of numbers, we deal with normal and custom ASCII values.

**Approach** :

Whenever there exists a custom ASCII value, use it instead of normal ASCII value.  
Apply **Kadane's algorithm** on the values obtained.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution{
    static String maxSum(String w,char x[],int b[], int n){
        HashMap<Character,Integer> map=new HashMap<Character,Integer>();
        for(int i=0;i<n;i++) map.put(x[i],b[i]);
        int max=0,sum=0,value=0,start=0,max_start=0,max_end=0;
        for(int i=0;i<w.length();i++){
            if(map.containsKey(w.charAt(i))) value=map.get(w.charAt(i));
            else value=w.charAt(i);
            if(!(sum+value>=value)){start=i;}
            sum=Math.max(sum+value,value);
            if(sum>max){ max=sum;max_start=start;max_end=i;}
        }
        return w.substring(max_start,max_end+1);
    }
}
```  
---  

12. #### [Subarray with given sum](https://practice.geeksforgeeks.org/problems/subarray-with-given-sum/0) :

**Question** :

Given an unsorted array A of size N that contains only non-negative integers, find a continuous sub-array which adds to a given number S and return the left and right index(1-based indexing) of that subarray.

In case of multiple subarrays, return the subarray indexes which comes first on moving from left to right.

Note:- Both the indexes in the array should be according to 1-based indexing. You have to return an arraylist consisting of two elements left and right. In case no such subarray exists return an array consisting of element -1.

**Intuition** :

This question uses the **sliding window approach** and checks if a subarray sum is equal to the given sum.

**Approach** :

Take two pointers **start** and **end** and variable **sum**.  
Whenever **sum < required_sum**, **increase end and add element** at corresponding index to sum.  
Whenever **sum > required_sum**, **increase start and subtract element** at corresponding index from sum.  
If **sum == required_sum** at any point, **return True**, **else return False**. 

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution
{
    static ArrayList<Integer> subarraySum(int[] arr, int n, int s) 
    {
        int start=0,sum=0;
        for(int i=0;i<n;i++){
            sum+=arr[i];
            while(sum>s && start<i){sum-=arr[start++];}
            if(sum==s) return new ArrayList<Integer>(List.of(start+1,i+1));
        }
        return new ArrayList<Integer>(List.of(-1));
    }
}
```  
---  

13. #### [Stock buy and sell](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell2615/1) :

**Question** :

The cost of stock on each day is given in an array A[] of size N. Find all the segments of days on which you buy and sell the stock so that in between those days your profit is maximum.

Note: Since there can be multiple solutions, the driver code will print 1 if your answer is correct, otherwise, it will return 0. In case there's no profit the driver code will print the string "No Profit" for a correct solution.

**Intuition** :

This was question whose solution was not that difficult to imagine but difficult to code.  
Whenever stock price rises, save the interval and print it, else ignore.

**Approach** :

This question has multiple nuances. We define variables for when we **buy, sell, an iterator and a flag**.  
**If we see a profit anywhere, we turn on the flag**. If we traverse the array and **never see a profit**, we print **No Profit**.  
We start traversing the array and check for loss first, so that we can catch the **No Profit** condition.  
**If we haven't traversed the whole array then we will see profit next** and **traverse till profits last and print the interval**.  
Then we **repeatedly traverse losses and profits untils we the whole array is covered**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    public void stockBuySell(int[] price, int n) {
        int i=0,buy=0,sell=0,flag=0;
        while(i<n-1){
            while(i<n-1 && price[i+1]<=price[i]) i++;
            if(i==n-1){
                if(flag==0) System.out.print("No Profit");
                break;
            }
            buy=i;
            flag=1;
            while(i<n-1 && price[i+1]>=price[i]) i++;
            sell=i;
            System.out.print("("+buy+" "+sell+") ");
        }
        System.out.println();
    }
}
```  
---  

14. #### [Largest subarray with 0 sum](https://practice.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1) :

**Question** :

Given an array having both positive and negative integers. The task is to compute the length of the largest subarray with sum 0.

**Intuition** :

We use the **prefix sum method** to first calculate the prefix sums. 
Whenver a value is repeated or we encounter a zero, it denotes a zero sum.  
We need to check for the largest interval. 

**Approach** :

We calculate the **prefix sums**.  
We create a **HashMap** and iterate through the array and **update the element in the map with it's latest index**.  
We define a **max** variable, traverse the array again and **find the difference of index of current element and its last occurence,  
 since it denotes an interval of zero sum**.    
**If the difference is greater than max, we update max.**  
Finally we also check **if max is greater than (value of 0 in map)+1 since that is a zero sum case as well**.  
Return **max**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class GfG
{
    int maxLen(int arr[], int n)
    {
        int sum=0;
        for(int i=0;i<n;i++){sum+=arr[i];arr[i]=sum;}
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<n;i++) map.put(arr[i],i);
        int max=0;
        for(int i=0;i<n;i++){
            if(map.get(arr[i])-i>max) max=map.get(arr[i])-i;
        }
        if(map.containsKey(0)){max=Math.max(max,map.get(0)+1);}
        return max;
    }
}
```  
---  

15. #### [Swapping pairs make sum equal](https://practice.geeksforgeeks.org/problems/swapping-pairs-make-sum-equal4142/1) :

**Question** :

Given two arrays of integers A[] and B[] of size N and M, the task is to check if a pair of values (one value from each array) exists such that swapping the elements of the pair will make the sum of two arrays equal.

**Intuition** :

If Sum1 is sum of first array and Sum2 is sum of second array,  
we have to search for elements x in array-1 and y in array-2 such that  
**Sum1-x+y=Sum2-y+x.**

**Approach** :

We find **sum1 of arr1** and **sum2 of arr2** and **save all the elements of first array in HashSet**.
First we check if **sum1-sum2 is even**, and **if not we return -1** since, to swap the **difference of sum must be even**.  
Travesing through the **2nd array** if **(sum1-sum2)/2+current_element** is **present in HashSet**, **we return 1**.
**Else, we return -1**.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    long findSwapValues(long A[], int n, long  B[], int m)
    {
        long sum1=0,sum2=0;
        HashSet<Long> set=new HashSet<Long>();
        for(int i=0;i<n;i++) {sum1+=A[i];set.add(A[i]);}
        for(int i=0;i<m;i++) sum2+=B[i];
        if((sum2-sum1) %2 !=0) return -1;
        for(int i=0;i<m;i++){
            if(set.contains((sum1-sum2)/2+B[i])) return 1;
        }
        return -1;
    }
}
```  
---  
16. #### [Minimum Number of Platforms Required for a Railway/Bus Station](https://practice.geeksforgeeks.org/problems/minimum-platforms/0) :

**Question** :

Given the arrival and departure times of all trains that reach a railway station, the task is to find the minimum number of platforms required for the railway station so that no train waits. We are given two arrays that represent the arrival and departure times of trains that stop.

**Intuition** :

We have to find the maximum number of consecutive trains/tasks that can occur.

**Approach** :

The best approach is to **sort both arrival arrays and departure arrays**.Then, **we traverse both arrays as if we are traversing a single sorted array** **till we reach the end of arrival array, since rest is departure**. While moving through both arrays **keep track of current trains/tasks and update a max variable**.  
**Return the max variable**.

**Complexity** :  

- Time complexity: $O(nlogn)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    static int findPlatform(int arr[], int dep[], int n)
    {
        Arrays.sort(arr);
        Arrays.sort(dep);
        int c=0,max=0,p=0,q=0;
        while(p<n){
            if(arr[p]<=dep[q]){p++;c++;}
            else{q++;c--;}
            if(c>max) max=c;
        }
        return max;
    }
    
}
```  
---  
17. #### [Largest Number formed from an Array](https://practice.geeksforgeeks.org/problems/largest-number-formed-from-an-array1117/1) :

**Question** :

Given an array of numbers, arrange them in a way that yields the largest value. For example, if the given numbers are {54, 546, 548, 60}, the arrangement 6054854654 gives the largest value. And if the given numbers are {1, 34, 3, 98, 9, 76, 45, 4}, then the arrangement 998764543431 gives the largest value.

**Intuition** :

The idea is to sort the elements in such a way that when they are added to a string, they give the max possible number as output.

**Approach** :

Using mergesort from Arrays.sort(), we just have to modify the comparator such that the array yeilds max number.  
For two numbers x and y we calculate x+y and y+x and then return -1 or 1 based upon which one is larger.  
We use str1.compareTo(str2) for comparing the two strings.

**Complexity** :  

- Time complexity: $O(nlogn)$  

- Space complexity: $O(1)$ 

```java
class Solution {
    String printLargest(String[] arr) {
        Arrays.sort(arr,new Comparator <String>(){
            @Override
            public int compare(String a,String b){
                return (a+b).compareTo(b+a)>0? -1:1;
            }
        });
        String ans="";
        for(String x:arr) ans+=x;
        return ans;
    }
}
```  
---  
18. #### [Trapping Rain Water](https://practice.geeksforgeeks.org/problems/trapping-rain-water-1587115621/1) :

**Question** :

Given an array arr[] of N non-negative integers representing the height of blocks. If width of each block is 1, compute how much water can be trapped between the blocks during the rainy season. 

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n2)$  

- Space complexity: $O(1)$ 

```java
class Solution{
    
    // arr: input array
    // n: size of array
    // Function to find the trapped water between the blocks.
    static long trappingWater(int arr[], int n) { 
        int left=0,i=0,cv=0,max=0;
        long vol=0;
        while(left<n){
            cv=arr[left];
            i=left+1;
            max=i;
            while(i<n){
                if(arr[i]>=arr[left]) break;
                if(arr[i]>arr[max]) max=i;
                i++;
            }
            if(i==n) while(++left<max)vol+=arr[max]-arr[left];
            else{
                while(++left<i) vol+=cv-arr[left];
            }
        }
        return vol;
    } 
}
```  
---  

</div>

