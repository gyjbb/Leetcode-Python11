# Leetcode-Python11

## 239. Sliding Window Maximum

May 24, 2023  4h

The eleventh day. Today we will learn about the queue and use it to solve problems.\
The challenges today are about ~~need to delete later~~.

## 239. Sliding Window Maximum
[leetcode](https://leetcode.com/problems/sliding-window-maximum/)\
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0239.%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%9C%80%E5%A4%A7%E5%80%BC.md)\
[video](https://www.bilibili.com/video/BV1XS4y1p7qj/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
Please note that we can't exceed the maximum time limite.\
When the window move one step forward, like a queue, we pop out the front item, and then push into the window a new item. And the queue always keep the number of k items. \
The trick here is that we always **keep the maximum number at the exit of the queue**, this is easy to pop anf other less value items are not important in the current window.\ When we push a new item in, we pop out all the items in the queue that are less than the current one. Then the largest number can be maintained at the exit of the queue.\
We would like our code to have these functions, and we can self define them to help us solve the problem:
> class MyQueue {\
> public:\
>    void pop(int value) { }\
>    void push(int value) { }\
>    int front() {return que.front();}\
> };\

设计单调队列的时候，以上pop，和push函数操作要保持如下规则：\
pop(value)：如果窗口移除的元素value等于单调队列的出口元素，那么队列弹出元素，否则不用任何操作\
push(value)：如果push的元素value大于入口元素的数值，那么就将队列入口的元素弹出，直到push元素的数值小于等于队列入口元素的数值为止\
保持如上规则，每次窗口移动的时候，只要问que.front()就可以返回当前窗口的最大值。\


