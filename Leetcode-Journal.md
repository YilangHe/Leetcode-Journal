[LeetCode 257](https://leetcode.com/problems/binary-tree-paths/description/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */

 /**
 backtracking:
 do dfs and if we reach the root, take a snapshot and store to the result list

  */
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        List<Integer> path = new ArrayList<>();

        bt(path, res, root);

        return res;

    }

    public void bt(List<Integer> path, List<String> res, TreeNode curr) {
        if(curr == null) return;
        path.add(curr.val);
        if(isLeaf(curr)) {
            // take a snapshot and store to the res
            String p = generatePath(path);
            res.add(p);
        } else {
            bt(path, res, curr.left);
            bt(path, res, curr.right);
        }

        path.remove(path.size() - 1);
    }

    public boolean isLeaf(TreeNode curr) {
        return curr != null && curr.left == null && curr.right == null;
    }

    public String generatePath(List<Integer> path) {
        StringBuilder sb = new StringBuilder();

        int len = path.size();

        for(int i = 0; i < len; i++) {
            if(i == 0) {
                sb.append(path.get(i));
            } else {
                sb.append('-');
                sb.append('>');
                sb.append(path.get(i));
            }
        }

        return sb.toString();
    }
}
```

[110. Balanced Tree](https://leetcode.com/problems/balanced-binary-tree/description/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    class Data {
        boolean isBala;
        int height;

        Data(boolean isBala, int height) {
            this.isBala = isBala;
            this.height = height;
        }
    }


    public boolean isBalanced(TreeNode root) {
        return dfs(root).isBala;
    }

    public Data dfs(TreeNode curr) {
        if(curr == null) {
            return new Data(true, 0);
        }

        Data left = dfs(curr.left);
        Data right = dfs(curr.right);

        boolean isBala = left.isBala && right.isBala && Math.abs(left.height - right.height) <= 1;

        return new Data(isBala, 1 + Math.max(left.height, right.height));
    }
}
```

