### 104. Maximum Depth of Binary Tree

```html
1. 
Q: What is the deapth of a tree:（深度）
A: It is from the root to the the node. root has 0 depth, but maybe 3 in height. 

Q: What is the height of a tree:(高度）
A: height of tree equals the height of root, from leaf (height is 0)to the root. increment.

Example: 
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
   
return its depth = 3.
```

```java

// from root going down, root is depth 1, then if root has children then it will be depth++, then its children's chidren then ++
// using a recursive
  public int maxDepth(TreeNode root) {
      int depthL = 0;
      int depthR = 0;
     if(root == null) {
      return 0;
     }
      if(root != null && root.left == null && root.right == null) {
         return 1;
      }
     if(root.left != null) {
         depthL = maxDepth(root.left)  + 1;   
     }
     
     if(root.left != null) {
         depthR = maxDepth(root.left)  + 1;   
     }
     return Math.max(depthR, depthL);
  }

```

```html
2. DFS root -> left (right) -> left.left (right->right)
Use a stack to solve this problem.

Stack has feature of pop(), and push()
We can use stack to push root left, and root right
Whenever we push once, we will add 1, because it going down

We also need to pop() the root, pop() the depth, in order to track the latest 
```
 
 
```java
public int maxDepth(TreeNode root) { 
    if(root == null) return 0;
    
    Stack<TreeNode> stackOfNode = new Stack<>();
    Stack<Integer> depths = new Stack<>();
    //1. intial stack 1  -  1
    stackOfNode.push(root);
    depths.push(1);
    
    //2. iterate stack
    int result = 0;
    while(!stack.isEmty()) {
        TreeNode currRoot = stack.pop();
        int currDepth = depths.pop();
        result = Math.max(result, currDepth);
        if(currRoot.right != null) {
            stackOfNode.push(currRoot.right);
            depths.push(currDepth + 1);
        }
        if(currRoot.left != null) {
            stackOfNode.push(currRoot.left);
            depths.push(currDepth + 1);
        }
    }
    return result;
}

```

```html
3. 
BFS root-> left -> right
using a queue

```

```java
public int maxDepth(TreeNode root) {
    if(root == null) return 0;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    int count = 0;
    while(!queue.isEMpty()) {
        
        int size = queue.size();
        while(size > 0 ) {
        TreeNode currHead = queue.poll(); //same level 
            if(currHead.left !=null) {
                queue.add(currHead.left);
            }
            if(currHead.right != null) {
                queue.add(currHead.right);
            }
            size--;
         }
        count++;
    }
    return count;
}
```
