---
layout: post
title: 二叉树的相关算法
subtitle: '"算法学习之路"'
date: 2019-10-13
author: 24253
header-img: img/Learning.jpg
catalog: true
tags:
  - 2019
---

> “🙉🙉🙉 ”

## 前言

总结二叉树的相关算法，未来可能会有扩展。

## 正文

### 二叉树深度遍历：

#### 前序：

递归：

```
let frontOrder = function(root, arrs = []) {
  if (root) {
    arrs.push(root.val);
    frontOrder(root.left, arrs);
    frontOrder(root.right, arrs);
  }
  return arrs;
};
```

非递归：

```
let frontOrder = function(root, arrs = []) {
  const result = [];
  const stack = [];
  let current = root;
  while (stack.length > 0 || current) {
    while (current) {
      result.push(current.val);
      stack.push(current);
      current = current.left;
    }
    current = stack.pop();
    current = current.right;
  }
  return result;
};
```

---

#### 中序：

递归：

```
let midOrder = function(root, arrs = []) {
  if (root) {
    midOrder(root.left, arrs);
    arrs.push(root.val);
    midOrder(root.right, arrs);
  }
  return arrs;
};
```

非递归：

```
let midOrder = function(root, arrs = []) {
  const result = [];
  const stack = [];
  let current = root;
  while (stack.length > 0 || current) {
    while (current) {
      stack.push(current);
      current = current.left;
    }
    current = stack.pop();
    result.push(current.val);
    current = current.right;
  }
  return result;
};
```

#### 后序：

递归：

```
let backOrder = function(root, arrs = []) {
  if (root) {
    backOrder(root.left, arrs);
    backOrder(root.right, arrs);
    arrs.push(root.val);
  }
  return arrs;
};
```

非递归：

```
let backOrder = function(root, arrs = []) {
  const result = [];
  const stack = [];
  let current = root;
  let last = null;              //标记上一个访问的节点
  while (stack.length > 0 || current) {
    while (current) {
      stack.push(current);
      current = current.left;
    }
    current = stack[stack.length-1];
    if(!current.right || current.right == last) {
        current = stack.pop();
        result.push(current.val);
        last = current;
        current = null;         //置空，继续弹栈
    } else {
        current = current.right;
    }
  }
  return result;
};
```

### 二叉树广度遍历：

```
const Bfs = function(root) {
    if(root == null) {
        return [];
    }
    let result = [];
    let stack = [root];
    while(stack.length > 0) {
        let current = stack.shift();
        result.push(current.val);
        if(current.left) {
            stack.push(current.left);
        }
        if(current.right) {
            stack.push(current.right);
        }
    }
}
```

---

## 后记

todo：以后增加 B 树、红黑树等介绍以及相关算法。

—— 24253 记于 2019-10-13
