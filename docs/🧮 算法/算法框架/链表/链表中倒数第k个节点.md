---
sidebar_position: 4
---

## 1 题目

输入一个链表，输出该链表中倒数第 k 个节点。为了符合大多数人的习惯，本题从 1 开始计数，即链表的尾节点是倒数第 1 个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

**示例：**

```txt
给定一个链表: 1->2->3->4->5, 和 k = 2.
返回链表 4->5.
```

> 和该题目类似的题目还有：
>
> 1. [19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list)。

## 2 解题思路

### 2.1 快慢指针

#### 2.1.1 问题分析

1. 定义两个指针，分别为慢指针 $slow$ 和快指针 $fast$。
2. 让快指针先走 $k$ 步。
3. 然后快慢指针同时移动，以后快慢指针的距离都为 $k$ 步，直到快指针为空，此时慢指针 $slow$ 即为倒数第 $k$ 个节点。

   ![](https://notebook.grayson.top/media/202107/2021-07-13_222646.png)

#### 2.1.2 参考代码

```java
/**
 * 剑指 Offer 22. 链表中倒数第 k 个节点（版本 2：双指针）
 * @param head  头结点
 * @param k 倒数节点个数
 * @return  链表中倒数第 k 个节点
 */
public ListNode getKthFromEndV2(ListNode head, int k) {
    //  快慢指针
    ListNode slow = head, fast = head;
    //  让快指针先走 k 步
    while (k > 0) {
        fast = fast.next;
        k--;
    }
    //  然后快慢指针同时移动，以后快慢指针的距离都为 k 步，直到快指针为空，此时慢指针即为倒数第 k 个节点
    while (fast != null) {
        slow = slow.next;
        fast = fast.next;
    }
    return slow;
}
```

## 3 参考文献

1. [剑指 Offer 22. 链表中倒数第 k 个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof)。
2. [19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list)。
3. [面试题 22. 链表中倒数第 k 个节点（双指针，清晰图解）](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/solution/mian-shi-ti-22-lian-biao-zhong-dao-shu-di-kge-j-11)。
