# 237. Delete Node in a Linked List
            
        Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.
        （在单链表上删除一个指定节点）
        Given linked list -- head = [4,5,1,9], which looks like following:

        4 -> 5 -> 1 -> 9  delete 1 node become  4 -> 5 -> 9
<br>
```
def deleteNode(self, node):
    node.val = node.next.val
    node.next = node.next.next
```