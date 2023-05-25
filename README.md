# Leetcode-Python11

## 239. Sliding Window Maximum

May 24, 2023  4h

The eleventh day. Today we will learn about the queue and use it to solve problems.\
The challenges today are about ~~need to delete later~~.

## 239. Sliding Window Maximum
[leetcode](https://leetcode.com/problems/sliding-window-maximum/)\
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0239.%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%9C%80%E5%A4%A7%E5%80%BC.md)\
[video](https://www.bilibili.com/video/BV1XS4y1p7qj/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
Please note that we can't exceed the maximum time limit.\
When the window moves one step forward, like a queue, we pop out the front item, and then push into the window a new item. And the queue always keeps the number of k items. \
The trick here is that we always **keep the maximum number at the exit of the queue**, this is easy to pop and other numbers less than this are not important in the current window. When we push a new item in, we pop out all the items in the queue that are less than the current one. Then the largest number can be maintained at the exit of the queue.\
We would like our code to have these functions, and we can self define them to help us solve the problem:
> class MyQueue {\
> public:\
>    void pop(int value) { }\
>    void push(int value) { }\
>    int front() {return que.front();}\
> };

其实队列没有必要维护窗口里的所有元素，只需要维护有可能成为窗口里最大值的元素就可以了。\
设计单调队列的时候，以上pop，和push函数操作要保持如下规则：\
- pop(value)：如果窗口移除的元素value等于单调队列的**出口**元素，那么队列弹出元素，否则不用任何操作\
- push(value)：如果push的元素value大于**入口**元素的数值，那么就将队列入口的元素弹出，直到push元素的数值小于等于队列入口元素的数值为止，此时push的元素是下一个可能的最大元素\
- 保持如上规则，每次窗口移动的时候，只要问que.front()就可以返回当前窗口的最大值。
```python
# use queue and self-defined functions pop(), push(), forunt() to solve this question:
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        que = MyQueue()
        result = []
        for i in range(k):  #先将前k的元素放进队列
            que.push(nums[i]) #use the self-defined push() function
        result.append(que.front())  #result 记录前k的元素的最大值
        for i in range(k, len(nums)):
            que.pop(nums[i-k])    #从滑动窗口移除最左边的元素
            que.push(nums[i])     #在滑动窗口里面加入最右面的元素
            result.append(que.front()) #记录对应的最大值
        return result

# define the 3 functions:
from collections import deque
class MyQueue:
    def __init__(self):
        self.queue = deque() 
    
    def pop(self, value):
        if self.queue and value == self.queue[0]: #数值等于队列出口元素
            self.queue.popleft() #将队列出口处数值弹出
    
    def push(self, value):
        while self.queue and value > self.queue[-1]: #push的数值大于入口元素的数值
            self.queue.pop() #将队列入口处数值弹出，没可能成为max的值没必要保存！
        self.queue.append(value) #将新数值从入口处加入
    
    def front(self): 
        return self.queue[0]   #返回队列出口处/前段/front数值，也是最大值
```
Attention for the deque():\
**queue[0] 出口/队列前端 popleft(): 从出口弹出元素\
queue[-1] 入口/队列后端 pop(): 从入口处弹出元素\
queue.append(value) #将数值从入口处加入**

##

