

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<img src="./Illustrations/sde.gif"/>
<div>


## Binary Tree


### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Height of Binary Tree](https://practice.geeksforgeeks.org/problems/height-of-binary-tree/1)

**Question** :

Given a binary tree, find its height.
Input:

    2
     \
      1
     /
    3
Output: 3 

**Approach** :

Return "h" for null node and for other cases return recursive function with value of "h" increased by one. Eventually max "h" will be pass through. 

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution {
    int height(Node node){
        return height(node,0);
    }
    int height(Node node,int h) {
        if(node==null) return h;
        return Math.max(height(node.left,h+1),height(node.right,h+1));
    }
}

// Alternate code with variable arguments.
// class Solution {
//     int height(Node node,int... h) {
//         if(node==null && h.length==0) return 0;
//         if(h.length==0) return Math.max(height(node.left,1),height(node.right,1));
//         if(node==null) return h[0];
//         return Math.max(height(node.left,h[0]+1),height(node.right,h[0]+1));
//     }
// }
```  
---  

2. #### [Number of leaf nodes](https://practice.geeksforgeeks.org/problems/count-leaves-in-binary-tree/1) :

**Question** :

Given a Binary Tree of size N, You have to count leaves in it. For example, there are two leaves in following tree
        
          1
        /   \
      10    39
     /
    5

**Approach** :

Returning 0 for a null node and 1 for a leaf node, and on other cases returning the sum of number of leaf nodes returned from left and right subtrees.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Tree
{
    int countLeaves(Node node) 
    {
        if(node ==null) return 0;
        if(node.left==null && node.right==null) return 1;
        return countLeaves(node.left)+countLeaves(node.right);
    }
}
```  
--- 
3. #### [Check if given Binary Tree is Height Balanced or Not](https://practice.geeksforgeeks.org/problems/check-for-balanced-tree/1) :

**Question** :

Given a binary tree, find if it is height balanced or not. 
A tree is height balanced if difference between heights of left and right subtrees is not more than one for all nodes of tree. 

A balanced binary tree:

           1
        /     \
      10      39
     /
    5

An unbalanced tree

         1
        /    
      10   
     /
    5

**Intuition** :

We just have to check the difference in height between the left and right subtree.

**Approach** :

Write a height function, and then at each node check if the difference if height between the left and right subtree is one or zero.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class Tree{
    int height(Node node, int h){
        if(node==null) return h;
        return Math.max(height(node.left,h+1),height(node.right,h+1));
    }
    boolean isBalanced(Node root){
        if(root==null) return true;
        if(Math.abs(height(root.left,0)-height(root.right,0))>1) return false;
        return isBalanced(root.left) && isBalanced(root.right);
    }
}
```  
--- 

4. #### [Given a binary tree, check whether it is a mirror of itself](https://practice.geeksforgeeks.org/problems/symmetric-tree/1) :

**Question** :

Given a Binary Tree. Check whether it is Symmetric or not, i.e. whether the binary tree is a Mirror image of itself or not.
Example of a symmetric binary tree: 

         5
       /   \
      1     1
     /       \
    2         2

Exmaple of a non symmetric binary tree:

         5
       /   \
      10     10
     /  \     \
    20  20     30


**Intuition** :

We have to travel down both the subtrees and check for symmetry.

**Approach** :

Travelling down the left subtree we check if the a similar symmetric node exists down the right subtree as well and if not return false. 

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class GfG{
    public static boolean isSymmetric(Node root){
        if(root==null) return true;
        return sym(root.left,root.right);
    }
    static boolean sym(Node left,Node right){
        if(left==null && right==null) return true;
        if((left==null ^ right==null)||(left.data!=right.data)) return false;
        return sym(left.left,right.right) && sym(left.right,right.left);
    }
}
```  
--- 
5. #### [Print Left View of Binary Tree](https://practice.geeksforgeeks.org/problems/left-view-of-binary-tree/1) :

**Question** :

Given a Binary Tree, print Left view of it. Left view of a Binary Tree is set of nodes visible when tree is visited from Left side. The task is to complete the function leftView(), which accepts root of the tree as argument.

Left view of following tree is 1 2 4 8.

           1
        /     \
       2       3
     /  \    /   \
    4   5   6     7
     \
      8   

**Intuition** :

Preorder traversal to save the leftmost node at each height.

**Approach** :

Write a height function that calculates the max height for a tree and init an array of that size. Do a preorder traversal and save the first node encountered at each level.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class Tree
{
    //Function to return list containing elements of left view of binary tree.
    ArrayList<Integer> leftView(Node root){
      ArrayList<Integer> sol=new ArrayList<Integer>();
      for(int i=0;i<height(root,0);i++) sol.add(Integer.MIN_VALUE);
      func(root,sol,0);
      return sol;
    }
    void func(Node node,ArrayList sol,int h){
        if(node==null) return;
        if((int)sol.get(h)==Integer.MIN_VALUE) sol.set(h,node.data);
        func(node.left,sol,h+1);
        func(node.right,sol,h+1);
    }
    int height(Node node, int h){
        if(node==null) return h;
        return Math.max(height(node.left,h+1),height(node.right,h+1));
    }
}
```  
--- 
6. #### [Print Bottom View of Binary Tree](https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1) :

**Question** :

Given a Binary Tree, The task is to print the bottom view from left to right. A node x is there in output if x is the bottommost node at its horizontal distance. The horizontal distance of the left child of a node x is equal to a horizontal distance of x minus 1, and that of a right child is the horizontal distance of x plus 1. 

             20
           /    \
         8       22
       /   \        \
     5       3       25
           /   \      
         10      14

For the above tree, the bottom view is 5 10 3 14 25.

If there are multiple bottom-most nodes for a horizontal distance from root, then print the later one in level traversal. For example, in the below diagram, 3 and 4 are both the bottommost nodes at horizontal distance 0, we need to print 4.

             20
           /     \
         8        22
       /   \     /   \
     5       3 4      25
            /    \      
         10       14

For the above tree the output should be 5 10 4 14 25.

**Intuition** :

For each unit of length we need to store the lowest and latest node.

**Approach** :

Make a function that calculates the width of the tree and make an array of that length to store the solution, also init an array to store the height of nodes in the solution array . While traversing down the tree, keeping track of the height, when we encounter a node, if the solution array doesnt have a node at this index along the length, or if the current node has a height greater than equal to the current node, we update the node in the solution array and its height in the height array. We return the solution array. 

**Complexity** :  

- Time complexity: $O(n log n)$  

- Space complexity: $O(n)$ 

```java
class Solution{
    //Function to return a list containing the bottom view of the given tree.
    public ArrayList <Integer> bottomView(Node root){
        int[] l=new int[2];
        findWidth(root,l,0);
        ArrayList sol=new ArrayList<Integer>(), h=new ArrayList<Integer>();
        for(int i=0;i<-1*l[0]+l[1]+1;i++){sol.add(0);h.add(0);}
        traverse(root,sol,h,-1*l[0],0);
        return sol;
        
    }
    //Treverses the binary tree and at each point along the width of the binary
    //check if the lowermost node is visible.
    void traverse(Node node,ArrayList<Integer> sol,ArrayList<Integer> height,int i,int h){
        if(node==null) return;
        if(sol.get(i)==0 ||height.get(i)<=h) {sol.set(i,node.data);height.set(i,h);}
        traverse(node.left,sol,height,i-1,h+1);
        traverse(node.right,sol,height,i+1,h+1);
    }
    //Finds the width of the binary tree. 
    void findWidth(Node root,int[] l,int i){
        if(root==null) return;
        if(i<l[0]) l[0]=i;
        if(i>l[1]) l[1]=i;
        length(root.left,l,i-1);
        length(root.right,l,i+1);
    }
}
```  
---  
7. #### [Diameter of a Binary Tree](https://practice.geeksforgeeks.org/problems/diameter-of-binary-tree/1) :

**Question** :

The diameter of a tree (sometimes called the width) is the number of nodes on the longest path between two end nodes. The diagram below shows two trees each with diameter nine, the leaves that form the ends of the longest path are shaded (note that there is more than one path in each tree of length nine, but no path longer than nine nodes). 

       1
     /  \
    2    3
Output: 3

         10
        /   \
      20    30
     /   \ 
    40   60
Output: 4

**Approach** :

For each node we have to check if the sum of depths of left and right subtrees is greater than max and update max accordingly.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class Solution {
    // Function to return the diameter of a Binary Tree.
    int diameter(Node root) {
        int[] max=new int[1];
        diameter(root,max);
        return max[0];
    }
    int diameter(Node node,int[] max){
        if(node==null) return 0;
        int left=diameter(node.left,max), right=diameter(node.right,max);
        if(left+right+1>max[0]) max[0]=left+right+1;
        return Math.max(left,right)+1;
    }
}
```  
---  
8. #### [Connect Nodes at Same Level](https://practice.geeksforgeeks.org/problems/connect-nodes-at-same-level/1) :

**Question** :

Given a Binary Tree, The task is to connect all the adjacent nodes at the same level starting from the left-most node of that level, and ending at the right-most node using nextRight pointer by setting these pointers to point the next right for each node.

        10                          10 ------> NULL
       / \                        /     \
      3   5       =>            3 ------> 5 --------> NULL
     / \   \                  /  \           \
    4   1   2                4 --> 1 ----->   2 -------> NULL


**Approach** :

We make a arraylist of nodes whose index reflect the height. In the arraylist we store the latest visited node at that height. When visit another node at the same height we attach the last visited node to the new node and update the new node in the array.

**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    //Function to connect nodes at same level.
    public void connect(Node root)
    {
        connect(root,new ArrayList<Node>(),0);
    }
    public void connect(Node node,ArrayList<Node> lists,int h){
        if(node==null)return;
        if(h+1>lists.size()) lists.add(node);
        else {lists.get(h).nextRight=node; lists.set(h,node);}
        connect(node.left,lists,h+1);
        connect(node.right,lists,h+1);
    }
}
```  
---  
9. #### [Level order traversal in spiral form](https://practice.geeksforgeeks.org/problems/level-order-traversal-in-spiral-form/1) :

**Question** :

Given a Binary Tree, the task is to print the Level order traversal of the Binary Tree in spiral form i.e, alternate order.

           10
         /     \
        20     30
      /    \
    40     60
    
Output: 10 20 30 60 40 

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Spiral{	
    ArrayList<Integer> findSpiral(Node root){
        ArrayList sol=new ArrayList<Integer>();
        ArrayList<ArrayList<Integer>> map=new ArrayList<ArrayList<Integer>>();
        func(root,map,0);
        for(int i=0;i<map.size();i++){
            if(i%2==0) Collections.reverse(map.get(i));
            sol.addAll(map.get(i));
        }
        return sol;
    }
    void func(Node node,ArrayList<ArrayList<Integer>> map,int h){
        if(node==null) return;
        if(h+1>map.size()) map.add(new ArrayList<Integer>(List.of(node.data)));
        else map.get(h).add(node.data);
        func(node.left,map,h+1);
        func(node.right,map,h+1);
    }
}
// Alternate code using list aiterator and descending iterator.
// class Spiral
// {
//     //Function to return a list containing the level order 
//     //traversal in spiral form.	
//     int height(Node root, int h){
//         if(root==null) return h;
//         return(Math.max(height(root.left,h+1),height(root.right,h+1)));
//     }
//     void makeSpiral(Node root, int h, ArrayList<LinkedList<Integer>> arr ){
//         if(root==null) return;
//         arr.get(h).addLast(root.data);
//         makeSpiral(root.left,h+1, arr);
//         makeSpiral(root.right,h+1, arr);
//     }
//     ArrayList<Integer> findSpiral(Node root) 
//     {
//         int h;
//         h=height(root,0);
//         ArrayList<LinkedList<Integer>> arr= new ArrayList<LinkedList<Integer>>();
//         for(int i=0;i<h;i++) arr.add(new LinkedList<Integer>());
//         ArrayList<Integer> sol=new ArrayList<Integer>();
//         makeSpiral(root,0,arr);
//         Iterator iter;
//         for(int i=0;i<h;i++){
//             if(i%2!=0) iter=arr.get(i).listIterator();
//             else iter=arr.get(i).descendingIterator();
//             while(iter.hasNext()) sol.add((Integer)iter.next());
//         }
//         return sol;
//     }
// }
```  
---  

</div>
