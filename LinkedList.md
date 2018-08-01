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
