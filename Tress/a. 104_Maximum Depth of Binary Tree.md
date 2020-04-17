### 104. Maximum Depth of Binary Tree

```html
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
 
