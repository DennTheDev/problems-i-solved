

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>

## Binary Search Tree
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Check for BST](https://practice.geeksforgeeks.org/problems/check-for-bst/1) :

**Question** :

Given the root of a binary tree. Check whether it is a BST or not.
Note: We are considering that BSTs can not contain duplicate Nodes.
A BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.


**Intuition** :

Everytime we encounter a non-null child we update the height and pass it on to the children. If we find the current node is null, we return the height. Else we return maximum of height of two children.

**Approach** :

We define a recursive function that has parameters as Node and height.
When the current node is null we return the current height.
Else we return the max of the recursive calls of left child and right child.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
public class Solution
{
    void addvals(Node node, ArrayList<Integer> arr){
        if(node==null) return;
        if(node.left!=null) addvals(node.left,arr);
        arr.add(node.data);
        if(node.right!=null) addvals(node.right,arr);
    }
    boolean isBST(Node root)
    {
        ArrayList<Integer> arr=new ArrayList<Integer>();
        addvals(root,arr);
        for(int i=1;i<arr.size();i++) {if(arr.get(i)<=arr.get(i-1)) return false;}
        return true;
        
    }
}
```  
---  
2. #### [Ceil in BST](https://practice.geeksforgeeks.org/problems/implementing-ceil-in-bst/1) :

**Question** :

Given a BST and a number X, find Ceil of X.
Note: Ceil(X) is a number that is either equal to X or is immediately greater than X.

**Intuition** :

While traversing through the BST we must find the largest element greater than or equal to the key.

**Approach** :

We traverse the BST while checking current node value to a variable initialised to Integer.MAX_VALUE. If the current value is greater than or equal to the key and but less than ceil variable, we update the ceil variable and continue traversing.

**Complexity** :  

- Time complexity: $O(h)$  

- Space complexity: $O(h)$ 

```java
class Tree {
    // Function to return the ceil of given number in BST.
    void func(Node node, int key, int[] sol){
        if(node==null) return;
        if(node.data>=key && node.data<sol[0]) sol[0]=node.data;
        if(key<node.data) func(node.left,key,sol);
        func(node.right,key,sol);
    }
    int findCeil(Node root, int key) {
        if (root == null) return -1;
        int [] sol=new int [1];
        sol[0]=Integer.MAX_VALUE;
        func(root,key,sol);
        return sol[0]==Integer.MAX_VALUE? -1:sol[0];
    }
}
```  
--- 

3. #### [Lowest Common Ancestor in a BST](https://practice.geeksforgeeks.org/problems/lowest-common-ancestor-in-a-bst/1) :

**Question** :

Given a Binary Search Tree (with all values unique) and two node values. Find the Lowest Common Ancestors of the two nodes in the BST.

**Intuition** :

If current node matches one of the keys, and one of the children return true, then the current key is the lowest common ancestor.
If the current node doesn't match one of the keys but both the children return true, then the current node is the lowest common ancestor.
Else return true if current node matches one of the keys or one of the children return true.

**Approach** :

We define a recursive function where we store the values of recursive calls of the children in two boolean and another boolean if the current node matches one of the keys. Current node matches one of the keys and one of the children return true, OR , if both children return true, then current node is the lowest common ancestor. Else return logical OR of values returned by children with current node matches one of the keys or not.  

**Complexity** :  

- Time complexity: $O(h)$  

- Space complexity: $O(h)$ 

```java
class BST
{   
    //Function to find the lowest common ancestor in a BST.
    boolean func(Node node, int n1, int n2, Node[] sol){
        if(node==null)return false;
        boolean a=func(node.left,n1,n2,sol);
        boolean b=func(node.right,n1,n2,sol);
        boolean c=node.data==n1 || node.data==n2;
        if((c && (a||b))||(a&&b)){
            sol[0]=node;
            return true;
        }
        return a||b||c;
    }
	Node LCA(Node root, int n1, int n2)
	{
        Node[] sol=new Node[1];
        func(root,n1,n2,sol);
        return sol[0];
    }
    
}
```  
--- 
4. #### [K-th Largest Element in BST](https://practice.geeksforgeeks.org/problems/kth-largest-element-in-bst/1) :

**Question** :

Given a Binary Search Tree (BST) and a positive integer k, find the k’th largest element in the Binary Search Tree. 
For example, in the following BST, if k = 3, then output should be 14, and if k = 5, then output should be 10. 

**Intuition** :

This question can be solved by traversing the larger elements of the BST and keeping track of the count.

**Approach** :

We make a recursive function that visits the rightmost node and while keeping track of the count, visits the root then left. If count equals K we save the current node value.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class Solution
{
    // return the Kth largest element in the given BST rooted at 'root'
    int func(Node node,int c,int k,int [] sol){
        if(node==null)return c;
        int x= func(node.right,c,k,sol);
        if(x<k){
            x+=1; 
            if (x==k) {sol[0]=node.data; return x;} 
            return func(node.left,x,k,sol);
        }
        return x;
        
    }
    public int kthLargest(Node root,int K)
    {
        int[] sol=new int[1];
        func(root,0,K,sol);
        return sol[0];
    }
}
```  
--- 


</div>
