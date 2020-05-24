学习笔记

合并两个有序链表:
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        head = ListNode(0)
        l3 = head
        while l1 or l2:
            if l1 and l2:
                val1 = l1.val
                val2 = l2.val
                if val1 < val2:
                    l3.next = ListNode(val1)
                    l1 = l1.next
                else:
                    l3.next = ListNode(val2)
                    l2 = l2.next
            elif l1:
                l3.next = ListNode(l1.val)
                l1 = l1.next
            else:
                l3.next = ListNode(l2.val)
                l2 = l2.next
            l3 = l3.next
        return head.next

两数之和：
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        d = {}
        for i, v in enumerate(nums):
            if target - v in d:
                return [i, d[target - v]]
            else:
                # 字典key存储值，value存储值对应的索引
                d[v] = i
