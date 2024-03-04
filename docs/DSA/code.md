# code

## Week1
1. **Arrays & Hashing**: Contains Duplicate, Valid Anagram, Two Sum
2. **Pointers**: Valid Palindrome, Two Sum II Input Array Is Sorted
3. **Sliding Window**: Best Time to Buy And Sell Stock, Longest Substring Without Repeating Characters
4. **Stack**: Valid Parentheses, Min Stack
5. **Binary Search**: Binary Search, Search a 2D Matrix
6. **LinkedList**: Reverse Linked List, Merge Two Sorted Lists
7. **Trees**: Invert Binary Tree, Maximum Depth of Binary Tree

### Contains Duplicate
``` py linenums="1"
def containsDuplicate(self, nums: List[int]) -> bool:
        array_set = {}
        for i in nums:
            if(i in array_set):
                return true
            array_set.add(i)
        return false
```
### Valid Anagram
``` py linenums="1"
def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        s_dict = {}
        t_dict = {}
        for i in range(len(s)):
            s_dict[s[i]] = s_dict.get(s[i],0)+1
            t_dict[t[i]] = t_dict.get(t[i],0)+1
        return s_dict==t_dict
```

### Two Sum
``` py linenums="1"
def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i, num in enumerate(nums):
            diff = target - num
            if diff in hashmap:
                return [hashmap[diff],i]
            hashmap[num] = i
        return [-1,-1]
```
### Valid Palindrome
``` py linenums="1"
def isPalindrome(self, s: str) -> bool:
        left, right = 0, len(s) - 1
        while(left < right):
            while(left<right and not s[left].isalnum()):
                left +=1
            while(left<right and not s[right].isalnum()):
                right -=1
            if(s[left].lower() != s[right].lower()):
                return False
            right -=1
            left +=1
        return True
```
### Two Sum II Input Array Is Sorted
``` py linenums="1"
def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left,right = 0, len(numbers) -1
        while( left < right):
            if((numbers[left] + numbers[right])==target):
                return [left+1,right+1]
            elif((numbers[left] + numbers[right])<target):
                left+=1
            else:
                right-=1
        return [-1,-1]
```
### Best Time to Buy And Sell Stock
``` py linenums="1"
def maxProfit(self, prices: List[int]) -> int:
        minprice = prices[0]
        maxprofit =0
        for price in prices:
            minprice = min(price,minprice)
            profit = price- minprice
            maxprofit = max(profit,maxprofit)
        return maxprofit
```
### Longest Substring Without Repeating Characters
``` py linenums="1"
def lengthOfLongestSubstring(self, s: str) -> int:
        hashset = set()
        left = 0
        maxlength = 0
        for right in range(len(s)):
            while(s[right] in hashset):
                hashset.remove(s[left])
                left+=1
            hashset.add(s[right])
            maxlength = max(right-left+1,maxlength)
        return maxlength
```
### Valid Parentheses
``` py linenums="1"
def isValid(self, s: str) -> bool:
        mapping = {'}':'{',"]":"[",")":"("}
        stack =[]
        for char in s:
            if char in mapping:
                topelement = stack.pop() if stack else "#"
                if mapping[char] != topelement:
                    return False
            else:
                stack.append(char)
        return not stack
```
### Min Stack
``` py linenums="1"
class MinStack:
    def __init__(self):
        self.stack = []
        self.minstack = []
    

    def push(self, val: int) -> None:
        self.stack.append(val)
        if(not self.minstack or val<=self.minstack[-1]):
            self.minstack.append(val)
    
 
    def pop(self) -> None:
        val = self.stack.pop()
        if(val==self.minstack[-1]):
            self.minstack.pop()
 

    def top(self) -> int:
        return self.stack[-1]
   

    def getMin(self) -> int:
        return self.minstack[-1]
```
### Binary Search
``` py linenums="1"
def search(self, nums: List[int], target: int) -> int:
        left,right = 0, len(nums) -1
        while(left <= right):
            mid = (left+right) // 2
            if(nums[mid] == target):
                return mid
            elif nums[mid] > target:
                right = mid - 1
            else:
                left = mid + 1
        return -1
```
### Search a 2D Matrix
``` py linenums="1"
 def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        top, bottom = 0, len(matrix) -1
        while(top<=bottom):
            row = (top+bottom)//2
            if(target<matrix[row][0]):
                bottom = row -1
            elif(target>matrix[row][-1]):
                top = row +1
            else:
                break
        if(not top<=bottom):
            return False
        row = (top+bottom)//2
        left, right = 0, len(matrix[row]) -1
        while(left<=right):
            mid =  (left+right)//2
            if(target == matrix[row][mid]):
                return True
            elif(target<matrix[row][mid]):
                right = mid-1
            else:
                left = mid+1
        return False
```
### Reverse Linked List
``` py linenums="1"
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        curr = head
        while(curr):
            temp = curr.next
            curr.next = prev
            prev = curr
            curr = temp
        return prev
```
### Merge Two Sorted Lists
``` py linenums="1"
def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        prevhead = ListNode(-1)
        curr  = prevhead
        while(list1 and list2):
            if(list1.val<=list2.val):
                curr.next = list1
                list1 = list1.next
            else:
                curr.next = list2
                list2 = list2.next
            curr = curr.next
        curr.next = list1 if list1 else list2
        return prevhead.next
```
### Invert Binary Tree
``` py linenums="1"
def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
         if not root:
             return None
         root.left,root.right = root.right,root.left
         self.invertTree(root.left)
         self.invertTree(root.right)
         return root
```
``` py linenums="1"
from collections import deque
 def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
        queue = deque([root])
        while queue:
            current = queue.popleft()
            current.left,current.right = current.right, current.left
            if current.left:
                queue.append(current.left)
            if current.right:
                queue.append(current.right)
        return root
```
### Maximum Depth of Binary Tree
``` py linenums="1"
def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        leftdepth = self.maxDepth(root.left)
        rightdepth = self.maxDepth(root.right)
        return max(leftdepth,rightdepth)+1
```
``` py linenums="1"
from collections import deque
def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        queue = deque([root])
        depth = 0
        while queue:
            depth += 1
            size = len(queue)
            for _ in range(size):
                current = queue.popleft()
                if current.left:
                    queue.append(current.left)
                if current.right:
                    queue.append(current.right)
        return depth
```

