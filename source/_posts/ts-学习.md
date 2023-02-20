---
title: ts-学习
date: 2023-02-17 20:04:36
tags: ts
categories:
---

## 一、Typescript

### 1、ts 介绍

是什么？

typescript 简称 ts，是 JavaScript 的超集。（JavaScript有的它都有）

typescript = type + JavaScript，在 js 基础上增加了类型支持。

typescript 是微软开发的开源编程语言，可以在 js 运行的地方运行。

`let age: number = 18`

解决了什么问题？有什么好处/优势？ 

![ts 优势](ts-学习/1676639577300.png)

- 减少改 bug、找 bug 的时间，提示开发效率。（理解于ts 、js 编程语言的机制）
- 程序中的代码有代码提示，随时随地的安全感，谁不喜欢呢。
- 强大的类型系统增加了代码的可维护性，使得更容易重构项目。
- 类型推断机制，享受语言的优势，谁不爱？
- 提供了强大的类型系统，大部分遵循 js 书写的习惯，同时也降低学习的成本。

vue3 的源码使用 ts 进行重写，angular 默认支持 ts，react 与 ts 完美配合~中大型前端项目首选编程语言。

怎么用？

浏览器、node.js 默认只支持 js 语言，ts 语言需要经过编译后进行运行。

① npm i -g tsc，tsc 模块包将 ts 代码编译成 js 代码，后可通过 node ××.js 进行运行。

② npm i -g ts-node , ts-node 模块包，内部偷偷地将 ts 代码进行编译后运行。

③ npm i -g nodemon，nodemon 工具包可以持续运行一个 js 文件，ts 文件应该也是可以的，我的电脑装了 nvm 管理多个 node 版本，可能是文件丢失，导致 ts-node 出现问题，也就执行不了 ts 文件。

### 2、ts 常用类型

