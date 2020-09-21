```java
//给定链表头结点 head，该链表上的每个结点都有一个 唯一的整型值 。 
//
// 同时给定列表 G，该列表是上述链表中整型值的一个子集。 
//
// 返回列表 G 中组件的个数，这里对组件的定义为：链表中一段最长连续结点的值（该值必须在列表 G 中）构成的集合。 
//
// 
//
// 示例 1： 
//
// 输入: 
//head: 0->1->2->3
//G = [0, 1, 3]
//输出: 2
//解释: 
//链表中,0 和 1 是相连接的，且 G 中不包含 2，所以 [0, 1] 是 G 的一个组件，同理 [3] 也是一个组件，故返回 2。 
//
// 示例 2： 
//
// 输入: 
//head: 0->1->2->3->4
//G = [0, 3, 1, 4]
//输出: 2
//解释: 
//链表中，0 和 1 是相连接的，3 和 4 是相连接的，所以 [0, 1] 和 [3, 4] 是两个组件，故返回 2。 
//
// 
//
// 提示： 
//
// 
// 如果 N 是给定链表 head 的长度，1 <= N <= 10000。 
// 链表中每个结点的值所在范围为 [0, N - 1]。 
// 1 <= G.length <= 10000 
// G 是链表中所有结点的值的一个子集. 
// 
// Related Topics 链表 
// 👍 52 👎 0


//java
//该题的做法就是经典的以空间换时间
//执行耗时:2 ms,击败了99.62% 的Java用户
//内存消耗:39 MB,击败了98.53% 的Java用户
//leetcode submit region begin(Prohibit modification and deletion)
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int numComponents(ListNode head, int[] G) {
        boolean[] flag = new boolean[10000]; //标记所有在G中出现过的数字，因为题目给的数组范围比较小，所以可以粗暴的用空间换时间，如果数组范围给的比较大，可以考虑使用hashSet或者map来标记出现过的数字
        for (int num: G) {
            flag[num] = true;
        }
        int ans = 0; //保存答案
        //考虑需要增加答案数的情况：
        //①：当前节点为标记节点且下一个节点不存在(null)
        //②：当前节点为标记节点且下一个节点不是标记节点
        //总结：必须满足当前节点为标记节点，然后判断当前节点的下一个节点是否存在，不存在直接答案加一，若存在则判断该节点是否为标记节点
        while(head != null) {
            if(flag[head.val] && (head.next == null || !flag[head.next.val])) {
                ans++;
            }
            head = head.next;
        }
        return ans;
    }
}
```

