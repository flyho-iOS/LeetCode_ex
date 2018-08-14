# 难度：easy

##  [237. Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/description/)

#### Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.（在单链表上删除一个指定节点）
> Given linked list -- head = [4,5,1,9], which lookzs like following:
>> 4 -> 5 -> 1 -> 9  delete 1 node become  4 -> 5 -> 9

#### 解题思路
```
    def deleteNode(node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        # 把指定的node.next的值赋值给node
        # 例：4 -> 5 -> 1 -> 9 变成 4->1->1->9 最后结果为4->1->9
        node.val = node.next.val
        node.next = node.next.next
```

## [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)

#### Reverse a singly linked list.(反转单链表)

#### 解题思路
```
    def reverseList(self, head):
        # 两个指针，记录当前的cur，记录cur的上一个node的pre
        cur = head
        pre = None
        while cur != None:
            # 用temp记录cur的下一个node，使下一步重设cur.next的时候不会丢失原来的cur.next
            temp = cur.next
            # 把cur.next指向pre
            cur.next = pre
            # pre指向cur
            pre = cur
            # cur指向原来的cur.next
            cur = temp
        return pre
```

## [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/) 

#### Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.（合并两个已排序的列表，返回一个新列表。）

#### Example:

> Input: 1->2->4, 1->3->4 <br>
> Output: 1->1->2->3->4->4

#### 解题思路
```
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if l1 is None and l2 is not None:
            return l2
        if l1 is not None and l2 is None:
            return l1
        if l1 is None and l2 is None:
            return None
        # 声明两个指针
        cur = temp = None
        if l1.val < l2.val:
            # l1和l2 谁小cur指向谁
            cur = l1
            # 然后l1 指向下一个node
            l1 = l1.next
        else:
            # 原理同上一步
            cur = l2
            l2 = l2.next

        temp = cur
        # 遍历l1 和 l2
        while l1 and l2:
            if l1.val > l2.val:
                cur.next = l2
                l2 = l2.next
            else:
                cur.next = l1
                l1 = l1.next
            cur = cur.next
            
        cur.next = l1 or l2
            
        return temp
```

## [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)

#### Given a linked list, determine if it has a cycle in it.（判断链表是否带环）

#### Follow up:
Can you solve it without using extra space?(空间复杂度要求为O(1))

```
	def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head is None:
            return False
        # fast指针每次两步，slow每次一步
        fast = slow = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
        	  # 如果fast和slow有重合，说明有环
            if slow == fast:
                return True
        return False
```

## [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/)

#### Remove all elements from a linked list of integers that have value val.（删除链表中指定值的node）

Example:

Input:  1->2->6->3->4->5->6, val = 6  
Output: 1->2->3->4->5

###### 解题思路
```
	def removeElements(self, head, val):
        
        # dummy指向
        dummy = ListNode(-1)
        dummy.next = head
        temp = dummy
        
        while temp and temp.next:
            if temp.next.val == val:
                temp.next = temp.next.next
            else:
                temp = temp.next
            
        return dummy.next
```

## [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

Given a linked list, remove the n-th node from the end of list and return its head.(删除倒数第N个结点)

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:

Given n will always be valid.

Follow up:

Could you do this in one pass? （只用一次遍历解决）

###### 解题思路
```
class Solution(object):
    def removeNthFromEnd(self, head, n):
       
        if not head or not head.next:
            return None
        # 定义dummy，dummy.next指向head    
        dummy = ListNode(0)
        dummy.next = head
        # 定义快慢指针
        slow = fast = dummy
        # 快指针先走n步，然后快慢指针一起走，直到fast.next不存在，此时slow.next指向的就是要删除的结点
        while fast.next:
            if n > 0:
                n -= 1
            else:
                slow = slow.next
            fast = fast.next
        # 特殊情况处理：如果slow指针没有动，停在dummy
        if slow == dummy:
        	  # dummy.next指向slow.next.next
            dummy.next = slow.next.next
        else:
            slow.next = slow.next.next
        return dummy.next
```

## [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

###### Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

###### 解题思路
```
class Solution:
    def mergeTwoLists(self, l1, l2):
        # cur是当前遍历位置的指针
        dummy = cur = ListNode(0)
        while l1 and l2:
			# cur指向l1和l2val小的
            if l1.val < l2.val:
                cur.next = l1
                l1 = l1.next
            else:
                cur.next = l2
                l2 = l2.next
            cur = cur.next
        # 遍历结束l1和l2可能两个都为空或其中一个为空，cur.next指向不为空的，即把剩余部分直接连接
        cur.next = l1 or l2
        return dummy.next
```

## [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Note: Do not modify the linked list.(找出一个带环的链表的环的起点)

Follow up:
Can you solve it without using extra space?

###### 解题思路
```
class Solution(object):
    def detectCycle(self, head):
        
        if not head:
            return None
        
        ## fast每次走两步，slow每次走一步
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            # 当fast和slow相遇，跳出循环
            if slow == fast:
                break
        else:
            return None
        # fast和slow随意选一个，然后head和slow分别各走一步，直到相遇，得到的就是环开始的点
        while head != slow:
            slow = slow.next
            head = head.next
        return head
```

## [83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)

Given a sorted linked list, delete all duplicates such that each element appear only once.
(删除重复节点)

######Example 1:

Input: 1->1->2
Output: 1->2
Example 2:

Input: 1->1->2->3->3
Output: 1->2->3

###### 解题思路
```
class Solution:
    def deleteDuplicates(self, head):
        
        temp = head
        whil temp and temp.next:
            if temp.val != temp.next.val:
                temp = temp.next
            else:
                temp.next = temp.next.next
        return head
```