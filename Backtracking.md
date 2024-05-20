

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

<img src="./Illustrations/sde.gif"/>

## Recursion and Backtracking
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Permutations of a given string](https://practice.geeksforgeeks.org/problems/permutations-of-a-given-string2041/1) :

**Question** :

Given a string S, the task is to write a program to print all permutations of a given string.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n!*n)$  

- Space complexity: $O(n)$ 

```java
class Solution {
    void func(String S,String str, int[] arr,HashSet<String> set){
        if(str.length()==arr.length) set.add(str);
        else{
            for(int i=0;i<arr.length;i++){
                if (arr[i]==0) {
                    arr[i]=1;
                    func(S,str+S.charAt(i),arr,set);
                    arr[i]=0;
                }
            }
        }
    }
    public List<String> find_permutation(String S) {
        HashSet<String> set=new HashSet<String>();
        func(S,"",new int[S.length()],set);
        List<String> soln=new ArrayList(set);
        Collections.sort(soln);
        return soln;
    }
}
```  
---  
2. #### [Rat in a Maze Problem](https://practice.geeksforgeeks.org/problems/rat-in-a-maze-problem/1) :

**Question** :

Consider a rat placed at (0, 0) in a square matrix of order N * N. It has to reach the destination at (N - 1, N - 1). Find all possible paths that the rat can take to reach from source to destination. The directions in which the rat can move are 'U'(up), 'D'(down), 'L' (left), 'R' (right). Value 0 at a cell in the matrix represents that it is blocked and rat cannot move to it while value 1 at a cell in the matrix represents that rat can be travel through it.
Note: In a path, no cell can be visited more than one time. If the source cell is 0, the rat cannot move to any other cell.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O$(3^(N2)^)

- Space complexity: $O(L * X)$, L = length of the path, X = number of paths 

```java
class Solution {
    static void bt(int[][]arr,ArrayList<String> result,String sol,int i,int j,int n){
        if(i>=n || j>=n || i<0 || j<0 || arr[i][j]==0) return;
        if(i==n-1 && j==n-1) {result.add(sol); return;}
        arr[i][j]=0;
        bt(arr,result,sol+"R",i,j+1,n);
        bt(arr,result,sol+"D",i+1,j,n);
        bt(arr,result,sol+"U",i-1,j,n);
        bt(arr,result,sol+"L",i,j-1,n);
        arr[i][j]=1;
    }
    public static ArrayList<String> findPath(int[][] m, int n) {
        ArrayList<String> result=new ArrayList<String>();
        bt(m,result,"",0,0,n);
        Collections.sort(result);
        return result;
    }
}
```  
---  

</div>
