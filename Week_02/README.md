## 本周作业

### 简单：

- 写一个关于 HashMap 的小总结。
    说明：对于不熟悉 Java 语言的同学，此项作业可选做。
- [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/description/)（亚马逊、Facebook、谷歌在半年内面试中考过）
- [两数之和](https://leetcode-cn.com/problems/two-sum/description/)（近半年内，亚马逊考查此题达到 216 次、字节跳动 147 次、谷歌 104 次，Facebook、苹果、微软、腾讯也在近半年内面试常考）
- [N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/description/)（亚马逊在半年内面试中考过）
- HeapSort ：自学 https://www.geeksforgeeks.org/heap-sort/

### 中等：

- [字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)（亚马逊在半年内面试中常考）
- [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)（亚马逊、字节跳动、微软在半年内面试中考过）
- [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)（字节跳动、谷歌、腾讯在半年内面试中考过）
- [N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)（亚马逊在半年内面试中考过）
- [丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)（字节跳动在半年内面试中考过）
- [前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)（亚马逊在半年内面试中常考）

## 下周预习

### 预习题目：

- [爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)
- [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)
- [Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)
- [子集](https://leetcode-cn.com/problems/subsets/)
- [N 皇后](https://leetcode-cn.com/problems/n-queens/)









## 本周作业

### 简单：

- 写一个关于 HashMap 的小总结。
    说明：对于不熟悉 Java 语言的同学，此项作业可选做。



HashMap是以键值对的形式存储的，如：<Key,Value>;



HashMap如何快速的找到元素存放的位置并得到数据呢？

- 是因为HashMap的内部是由Hash实现的，用Hash来计算要存储的位置，可以快速的拿到数据存放的位置。
- 如果多个元素都在同一个HashMap的位置的话，就会自动形成一个链接的形式，一个接着一个。









HashMap取出复杂度是O(1)的；



- [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/description/)（亚马逊、Facebook、谷歌在半年内面试中考过）



```java
class Solution {
    public boolean isAnagram(String s, String t) {
        Map<Character,Integer> map = new HashMap<Character,Integer>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            map.put(c,map.getOrDefault(c,0) + 1);
        }

        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);

            map.put(c,map.getOrDefault(c,0) - 1);

            if(map.get(c) < 0){
                return false;
            }else if(map.get(c) == 0){
                map.remove(c);
            }

        }

        return map.isEmpty();
    }
}
```

- [两数之和](https://leetcode-cn.com/problems/two-sum/description/)（近半年内，亚马逊考查此题达到 216 次、字节跳动 147 次、谷歌 104 次，Facebook、苹果、微软、腾讯也在近半年内面试常考）

```java
 public int[] twoSum(int[] nums, int target) {

        Map<Integer,Integer> map = new HashMap<Integer,Integer>();

        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i],i);
            if(map.containsKey(target - nums[i])){
                return new int[]{map.get(target - nums[i]),i};
            }
            map.put(nums[i],i);
        }
        return new int[]{};
    }
```

- [N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/description/)（亚马逊在半年内面试中考过）



```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> result = new ArrayList<>();

        build(result,root);

        return result;
    }

    public void build(List<Integer> result,Node root){

        if(root==null) return;
         result.add(root.val);

        for(int i=0;i<root.children.size();i++){
            build(result,root.children.get(i));
        }
    }
}
```

- HeapSort ：自学 https://www.geeksforgeeks.org/heap-sort/



### 中等：



- [字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)（亚马逊在半年内面试中常考）



- [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)（亚马逊、字节跳动、微软在半年内面试中考过）

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        build(result,root);
        return result;
    }

    public void build(List result,TreeNode root){
        if(root==null) return;
        
        build(result,root.left);
        result.add(root.val);
        build(result,root.right);
    }
}
```

- [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)（字节跳动、谷歌、腾讯在半年内面试中考过）



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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        build(result,root);
        return result;
    }

    public void build(List list,TreeNode root){
        
        if(null == root) return;
        list.add(root.val);
        build(list,root.left);
        build(list,root.right);
        
    }

}
```

- [N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)（亚马逊在半年内面试中考过）



- [丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)（字节跳动在半年内面试中考过）



- [前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)（亚马逊在半年内面试中常考）