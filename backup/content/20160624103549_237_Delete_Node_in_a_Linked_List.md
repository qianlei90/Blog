Title: 237. Delete Node in a Linked List
Date: 2016-06-24 10:35:49
Category: LeetCode
Tags:
Slug: 237_Delete_Node_in_a_Linked_List
Author: Lemon Tree

## Question

    Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.
    Supposed the linked list is `1 -> 2 -> 3 -> 4` and you are given the third node with value 3, the linked list should become `1 -> 2 -> 4` after calling your function.

## Solution

  最初的思路还在想，因为是单向链表，怎么去找之前的节点？单向链表是没法找到之前的节点的啊。想了很久，以为有什么技术是可以做到的，但回想了很久数据结构的课程，里面也没有提到一星半点。
  当前节点是不能删除的，因为上一个节点会指向当前节点，但上一个节点没法修改。所以正确的思路应该是删除的是下一个节点。

### Show me the code

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val, node.next = node.next.val, node.next.next
```

\- 完 -
