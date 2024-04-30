## 0、前言

因为最近在开发一个新功能，就是chatgpt聊天后解雇哦的出现要逐字显示的，我是用的是setinterval 加上回调的形式去显示的，但是同事说可以使用requestAnimationFrame去实现。同事之前面试的时候有面试官提出说1w条数据同时上来如何优化的问题，我回答说缓存、分页、预加载等措施，面试官最后说还可以使用requestAnimationFrame来实现这个功能。所以引起了我的好奇心，想看看这玩意儿到底都有什么应用场景

## 一、是什么

是js中**`window.requestAnimationFrame()`**一个公用方法

## 二、有啥用

告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。

使用场景：

- 1.游戏开发
- 2.用户界面动画

前端动画方案有哪些？

主要分类为`css动画`和`js动画`，如下细分：

- `css`动画
  - `transition`过渡动画
  - `animation`直接动画（搭配`@keyframes`）
- `js`动画
  - `setInterval`或`setTimeout`定时器（比如不停地更改`dom元素`的位置，使其运动起来）
  - `canvas`动画，搭配`js`中的定时器去运动起来（`canvas`只是一个画笔，然后我们通过定时器会使用这个画笔去画画-动画）
  - `requestAnimationFrame动画（js动画中的较好方案）`

- 3.数据可视化

## 三、怎么用

```
window.requestAnimationFrame(callback)
```

```
function animate(){
   //设置终止条件
   //编写操作动画
   //...
   //请求下一次重绘
   window.requestAnimationFrame(animate)
}
window.requestAnimationFrame(animate)
```

## 四、分析

优点：

不会抖动

缺点：

不能控制控制帧的时间

[参考文档：写的很好，值得一看](https://zhuanlan.zhihu.com/p/600296111)
