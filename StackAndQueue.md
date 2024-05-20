

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>

## Stack and Queue
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Parenthesis Checker](https://practice.geeksforgeeks.org/problems/parenthesis-checker2744/1?utm_source=gfg&utm_medium=article&utm_campaign=bottom_sticky_on_article) :

**Question** :

Given an expression string x. Examine whether the pairs and the orders of {,},(,),[,] are correct in exp.
For example, the function should return 'true' for exp = [()]{}{[()()]()} and 'false' for exp = [(]).

**Intuition** :

If we read a open bracket, we add that to the stack, when we read a matching closing bracket we pop the last opening bracket.
If the stack is empty, all brackets must be in correct order.

**Approach** :

We add **push open parantheses to stack**, **if we encounter closed parantheses** and **we have a matching closed parantheses on the top** of stack, **we pop** the top of stack. **If the stack top doesnt match the closing parantheses** or **we encounter a closing parantheses when stack is empty we return false**. 

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    //Function to check if brackets are balanced or not.
    static boolean ispar(String x)
    {
        char c='a', cc='a';
        Stack<Character> stack=new Stack<Character>();
        for(int i=0;i<x.length();i++){
            c=x.charAt(i);
            if(c == 40 || c == 91 || c == 123) stack.push( c );
            else{
                if(stack.empty()) return false;
                cc=stack.peek();
                if((cc==40 && c==41)|| (cc==91 && c==93)||(cc==123 && c==125))stack.pop();
                else return false;
            }
        }
        return stack.empty();
    }
}
```  
---  
2. #### [Merge Overlapping Intervals](https://practice.geeksforgeeks.org/problems/8a644e94faaa94968d8665ba9e0a80d1ae3e0a2d/1/) :

**Question** :

Given a set of time intervals in any order, merge all overlapping intervals into one and output the result which should have only mutually exclusive intervals.
For example,

Intervals = {{1,3},{2,4},{6,8},{9,10}}

Output: {{1, 4}, {6, 8}, {9, 10}}

Intervals = {{6,8},{1,9},{2,4},{4,7}}

Output: {{1, 9}}

**Intuition** :

We have to sort the intervals in the increasing order of their start time. Then we have to merge subsequent intervals that are enclosed or overlapping with current interval, by updating the current interval.

**Approach** :

First **we sort all the intervals on the basis of their start times**. 
Then we set a variable **c as 0**. This represents the **index of the last non-overlapping interval**.
Iterating through the intervals **if the current interval lies in or overlaps last non-overlapping interval**, **we update the last non-overlapping interval and continue iterating**.
**Else we increase c** and **set the new non-overlapping interval as current interval**.

**Complexity** :  

- Time complexity: $O(n log n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    public int[][] overlappedInterval(int[][] arr)
    {
        if(arr.length==1)return arr;
        Arrays.sort(arr,new Comparator<int[]>(){
            @Override
            public int compare(int[] a,int[] b){
                return a[0]<b[0]?-1:1;
            }
        });
        int c=0;
        for(int i=1;i<arr.length;i++){
            if(arr[i][0]>arr[c][1]) arr[++c]=arr[i];
            else if(arr[i][1]>arr[c][1]) arr[c][1]=arr[i][1];
        }
        int[][] sol=Arrays.copyOf(arr,c+1);
        return sol;
    }
}
```  
---  

3. #### [Stock span problem](https://practice.geeksforgeeks.org/problems/stock-span-problem-1587115621/1/) :

**Question** :

The stock span problem is a financial problem where we have a series of N daily price quotes for a stock and we need to calculate the span of the stock’s price for all N days. The span Si of the stock’s price on a given day i is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the current day is less than its price on the given day.

price[] = [100 80 60 70 60 75 85] 

Output: 1 1 1 2 1 4 6

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    //Function to calculate the span of stockâ€™s price for all n days.
    public static int[] calculateSpan(int arr[], int n)
    {
        Stack<Integer> stack=new Stack<Integer>();
        int[] sol=new int[n];
        int c=1;
        stack.push(0);
        sol[0]=1;
        for(int i=1;i<n;i++){
            c=1;
            while(!stack.empty()&&arr[stack.peek()]<=arr[i]) c+=sol[stack.pop()];
            stack.push(i);
            sol[i]=c;
        }
        return sol;
    }
    
}
```  
---  
4. #### [Next Greater Element](https://practice.geeksforgeeks.org/problems/next-larger-element-1587115620/1) :

**Question** :

Given an array arr[ ] of size N having elements, the task is to find the next greater element for each element of the array in order of their appearance in the array.
Next greater element of an element in the array is the nearest element on the right which is greater than the current element.
If there does not exist next greater of current element, then next greater element for current element is -1. For example, next greater of the last element is always -1.

arr[]= [6 8 0 1 3]

Output:
8 -1 1 3 -1

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    //Function to find the next greater element for each element of the array.
    public static long[] nextLargerElement(long[] arr, int n)
    { 
        Stack<Integer> stack=new Stack<Integer>();
        stack.push(0);
        for(int i=1;i<n;i++){
            while(!stack.empty()&&arr[i]>arr[stack.peek()]) arr[stack.pop()]=arr[i];
            stack.push(i);
        }
        while(!stack.empty()) arr[stack.pop()]=-1;
        return arr;
    } 
}
```  
---  
5. #### [Queue using Stacks](https://practice.geeksforgeeks.org/problems/queue-using-stack/1) :

**Question** :

We are given a stack data structure with push and pop operations, the task is to implement a queue using instances of stack data structure and operations on them.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(1)$ for enqueue and  $O(n)$ for dequeue 

- Space complexity: $O(1)$ for both enqueue and dequeue 

```java
class Queue
{
    Stack<Integer> input = new Stack<Integer>(); 
    Stack<Integer> output = new Stack<Integer>(); 
    
    /*The method pop which return the element poped out of the stack*/
    int dequeue()
    {
	    if(input.isEmpty()) return -1;
	    while(!input.isEmpty()) output.push(input.pop());
	    int x=output.pop();
	    while(!output.isEmpty()) input.push(output.pop());
	    return x;
    }
	
    /* The method push to push element into the stack */
    void enqueue(int x)
    {
	    input.push(x);	
    }
}
```  
---  

6. #### [Implement Stack using Queues](https://practice.geeksforgeeks.org/problems/stack-using-two-queues/1) :

**Question** :

Given a Queue data structure that supports standard operations like enqueue() and dequeue(). The task is to implement a Stack data structure using only instances of Queue and Queue operations allowed on the instances.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(1)$ for push() and $O(n)$ for pop()  

- Space complexity: $O(1)$ for both push() and pop() 

```java
class Queues
{
    Queue<Integer> q1 = new LinkedList<Integer>();
    Queue<Integer> q2 = new LinkedList<Integer>();
    
    //Function to push an element into stack using two queues.
    void push(int a)
    {
	    q1.add(a);	
    }
    
    //Function to pop an element from stack using two queues. 
    int pop()
    {
	    if(q1.isEmpty()) return -1;
	    while(q1.size()>1) q2.add(q1.remove());
	    int x=q1.remove();
	    while(q2.size()>0) q1.add(q2.remove());
	    return x;
    }
	
}
```  
---  

</div>
