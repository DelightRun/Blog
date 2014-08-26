---
layout: post
title: "C++头文件内容建议"
date: 2014-05-22 22:31:06 +0800
comments: true
categories: C++
---

以下列出一些关于C++头文件内容的建议

>本文内容摘自《C++程序设计语言》

<!-- more -->

###可以包含
+ 命名名字空间          namespace N {/\*...\*/}
+ 类型定义              struct Point { int x,y; };
+ 模板声明              template<class T> class Z;
+ 模板定义              template<class T> class V {/\*...\*/};
+ 函数声明              extern int strlen(const chari\*);
+ inline函数定义        inline char get(char\* p) { return \*p++; }
+ 数据声明              extern int a;
+ 常量定义              const float pi = 3.141593;
+ 枚举                  enum Light { red,yellow,green };
+ 名字声明              class Matrix;
+ 包含指令              #include <iostream>
+ 宏定义                #define VERSION 12
+ 条件编译指令          #ifdef \__cplusplus
+ 注释                  /\* comment \*/

###绝不该有
+ 常规的函数定义        char get(char\* p) { return \*p++; }
+ 数据定义              int a;
+ 聚集量定义            short tbl[] = {1,2,3};
+ 无名名字空间          namespace {/\*...\*/}
+ 导出的模板定义        export template<class T> f(T t) {/\*...\*/}
