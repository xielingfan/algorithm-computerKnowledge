#### [117. 填充每个节点的下一个右侧节点指针 II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)



# 题目描述

给定一个二叉树

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。

进阶：

你只能使用常量级额外空间。
使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。


# 示例

```

输入：root = [1,2,3,4,5,null,7]
输出：[1,#,2,3,#,4,5,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。
```
# 代码

```java
//java
//层次遍历
class Solution {
    public Node connect(Node root) {
        if(root == null) return root;
        Deque<Node> queue = new LinkedList<>();
        queue.offerLast(root);
        while (!queue.isEmpty()){
            int len = queue.size();
            Node last = null;
            for(int i = 0; i < len; ++i){
                Node tmp = queue.pollFirst();
                if(tmp.left != null) queue.offerLast(tmp.left);
                if(tmp.right != null) queue.offerLast(tmp.right);
                if(i != 0) last.next = tmp;
                last = tmp;
            }
        }
        return root;
    }
}
```

```java
//java
//cur 指针利用 next 不停的遍历当前层。
//如果 cur 的孩子不为 null 就将它接到 tail 后边，然后更新tail。
//当 cur 为 null 的时候，再利用 dummy 指针得到新的一层的开始节点。
//dummy 指针只是为了处理头结点的情况，它并不属于当前链表。
class Solution {
    public Node connect(Node root) {
        Node cur = root;
        while(cur != null){
            Node dummy = new Node();
            Node tail = dummy;
            while (cur != null){
                if(cur.left != null){
                    tail.next = cur.left;
                    tail = tail.next;
                }
                if(cur.right != null){
                    tail.next = cur.right;
                    tail = tail.next;
                }
                cur = cur.next;
            }
            cur = dummy.next;
        }
        return root;
    }
}
```
