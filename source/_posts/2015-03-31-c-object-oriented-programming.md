---
layout: post
title: "面向对象的C编程"
date: 2015-03-31 19:25:38 +0800
comments: true
categories: C
---

> 翻译自[C Object Oriented Programming](http://nullprogram.com/blog/2014/10/21/)

<!--more-->

面向对象编程，尤其是多态性，对大型复杂软件的开发至关重要。
没有面向对象编程，则分离不同系统组件将是非常困难的。
C语言并不支持面向对象，所以大型C程序总是发展其自己的构建方式，
而不是单纯地依照原始的C语言准则。
比较有代表性的大型C语言项目的例子如Linux内核、BSD内核和SQLite

一个简单的例子
=============

假设你打算写一个函数`pass_match()`，该函数接受一个输入流、一个输出流和一个模式串。
这个函数的工作有点像`grep`命令，它将输入流中与模式串相匹配的行输出至输出流。
模式串是一个shell风格Glob模式串，该串与[POSI fnmatch()](http://man7.org/linux/man-pages/man3/fnmatch.3.html)函数的模式串语法一致。
整个函数接口如下：

~~~c
void pass_match(FILE *in, FILE *out, const char *pattern);
~~~

Glob风格模式串非常简单，所以不需要进行预编译（正则表达式一般需要预编译）。

一段时间后，我们的客户想让程序除了shell风格Glob字符串外还支持正则表达式。
为了性能需要，正则表达式需要被预编译，所以不能直接作为模式串传递给我们的函数，取而代之的将是一个[POSIX regex\_t](http://man7.org/linux/man-pages/man3/regexec.3.html)对象。
对本问题，一种快速但不怎么优雅的实现如下

~~~c
void pass_match(FILE *in, FILE *out, const char *pattern, regex_t *re);
~~~

需要注意的是，`pattern`和`re`参数总有一个会是NULL。不过这个实现非常丑陋而且不便于扩展。
试想，如果我们需要更多种不同的匹配器该怎么办？所以我们需要一种只接受一个对象的实现，而不是像现在这样同时存在`pattern`和`re`对象。如果可能，我们还希望我们的对象可以扩展以适应各种不同的匹配器。

支持通用的匹配函数
=================

一种常见的用于扩展C语言函数的方式是向函数传递函数指针。
例如，作为比较器的`qsort()`函数的最后一个变量就是一个函数指针。

对于我们的`pass_match()`函数，这个函数指针指向的函数应该可以接受一个字符串并返回一个布尔值以表明该字符串是否该被我们的`pass_match()`函数传递至输出流。
我们对输入流的每一行调用该函数。

{% codeblock lang:c %}
void pass_match(FILE *in, FILE *out, bool (*match)(const char *));
{% endcodeblock %}

不过，这种实现同`qsort()`一样——缺乏上下文环境。`match`所指向的函数需要一个模式串或者一个`regex_t`对象来操作。在其他语言中，这种对上下文环境的依赖可以作为一个闭包附加到函数，但是C语言并不支持闭包。一种简单粗暴地实现方式是使用全局变量，但这并不值得提倡。

~~~c
static regexi_t regex;    // 非常差的方式！

bool regex_match(const char *string)
{
    return regexec(&regex, string, 0, NULL, 0) == 0;   
}
~~~

因为全局变量的存在，`pass_match()`既不是可重入的也不是线程安全的。
我们将学习GNU的`qsort_r()`函数，接受一个上线文变量给我们的匹配函数，类似于一个闭包。

~~~c
void pass_match(FILE *in, FILE *out, 
        bool (*match)(const char *, void *), void *context);
~~~

其中context指针将作为匹配函数的第二个参数以用来给其提供上下文环境，因此我们就用不到全局变量了。
这种实现对于许多简单情况是足够用了，我们的`pass_match()`接口也可以处理不同匹配函数的情况。

但是，我们为何不能将一个函数及其上下文环境打包为一个对象呢？

更抽象的做法
===========

我们为何不能将上下文参数放入一个结构体并对其开发接口？这里我们使用了**结构体+联合**的的方式：

~~~c
enum filter_type { GLOB, REGEX };

struct filter {
    enum filter_type type;
    union {
        const char *pattern;
        regex_t regex;
    } context;
};
~~~

然后我们定义一个操作该结构体的函数：`filter_match()`。它检查`type`成员并调用正确的函数来执行匹配工作。

~~~c
bool filter_match(struct filter *filter, const char *string)
{
    switch (filter->type) {
    case GLOB:
        return fnmatch(filter->context.pattern, string, 0) == 0;
    case REGEX:
        return regexec(&filter->context.regex, string, 0, NULL, 0) == 0;
    }
    abort();    // handle errors
}
~~~

现在我们回到我们的`pass_match()`函数，它的接口现在应该如下所示，这也是本文对`pass_match()`函数接口形式和实现的最后一次修改。

~~~c
void pass_match(FILE *input, FILE *output, struct filter *filter);
~~~

现在我们的`pass_match()`无需关注匹配函数是如何工作的了，这样也为我们将来的扩展提供了可能。现在的`pass_match()`函数只是简单地调用`filter_match()`函数。但是，我们使用了`switch`语句和`union`，这样虽然能工作但并不优美，而且修改起来非常麻烦（如、我们添加一钟新的匹配器类型就需要改动多处），所以我们要进一步改进。

方法（Method）
============

既然使用`switch`语句非常的不好，那我们就干脆将函数指针放入结构体：

~~~c
struct filter {
    bool (*match)(struct filter *, const char *);
};
~~~

注意到我们`filter`结构体将其自身作为第一个参数传递给了`match()`函数。在OOP语言中，这就相当于实现了`this`指针。现在，我们将这样写`filter_match()`函数

~~~c
bool filter_match(struct filter *filter, const char *string)
{
    return filter->match(filter, string);
}
~~~

注意到，我们的`filter`结构体只是个框架，我们还是缺少真正的上下文参数，一个模式串或者一个`regex`对象。这两者将会作为不同的结构体定义，而其公共部分正是`filter`结构体。

~~~c
struct filter_regex {
    struct filter filter;
    regex_t regex;
}

struct filter_glob {
    struct filter filter;
    const char *pattern;
}
~~~

**注意：`filter`结构体必须作为上述结构体的第一个成员**。这个技巧叫做*结构双关*，英文名称*type punning*。结构体的第一个成员一定位于结构体内存区域的开始处，所以指向`struct filter_glob`的指针也是其第一个成员变量的指针，即指向`struct filter`的指针。这种做法是不是有点类似于继承？

现在，我们的两个结构体类型——`filter_regex`和`filter_glob`都需要它们各自的匹配函数。

~~~c
static bool
method_match_regex(struct filter *filter, const char *string)
{
    struct filter_regex *regex = (struct filter_regex *) filter;
    return regexec(&regex->regex, string, 0, NULL, 0) == 0;
}

static bool
method_match_glob(struct filter *filter, const char *string)
{
    struct filter_glob *glob = (struct filter_glob *) filter;
    return fnmatch(glob_pattern, string, 0) == 0;
}
~~~

使用前缀`method_`是为了指明它们的用途。声明为`static`是为了使其为文件私有，程序的其他部分只能通过结构体中的函数指针对其进行访问。同时，这也意味着我们需要一些构造函数来初始化那些函数指针。

~~~c
struct filter *filter_regex_create(const char *pattern)
{
    struct filter_regex *regex = malloc(sizeof(*regex));
    regcomp(&regex->regex, pattern, REG_EXTENDED);
    regex->filter.match = method_match_regex;
    return &regex->filter;
}

struct filter *filter_glob_create(const char *pattern)
{
    struct filter_glob *glob = malloc(sizeof(*glob));
    glob->pattern = pattern;
    glob->filter.match = method_match_glob;
    return &glob->filter;
}
~~~

以上，我们就完成了对接口的封装，而且从用户的角度来讲其足够健壮、可扩展并且易于使用。

清理
===

以上还没完，我们的正则表达式匹配器在使用完后还需要进行清理，但是我们的用户并不知道如何正确执行清理操作。所以我们添加`free()`方法。

~~~c
struct filter {
    bool (*match)(struct filter *, const char *);
    void (*free)(struct filter *);
};

void filter_free(struct filter *filter)
{
    return filter->free(filter);
}
~~~

同时，每种匹配器的清理函数，将在其构造函数内进行指定。

~~~c
static void
method_free_regex(struct filter *f)
{
    struct filter_regex *regex = (struct filter_regex *) f;
    regfree(&regex->regex);
    free(f);
}

static void
method_free_glob(struct filter *f)
{
    free(f);
}
~~~

当然，上述只是个简单的事例，你还可以在其中添加其他的清理步骤。

对象组件
=======

很多时候使用组件而不是继承是一个好的实践。现在我们实现一个AND操作，该操作当且仅当两个子匹配器都匹配时返回真。

~~~c
struct filter_and {
    struct filter filter;
    struct filter *sub[2];
};

static bool
method_match_and(struct filter *f, const char *s)
{
    struct filter_and *and = (struct filter_and *) f;
    return filter_match(and->sub[0], s) && filter_match(and->sub[1], s);
}

static void
method_free_and(struct filter *f)
{
    struct filter_and *and = (struct filter_and *) f;
    filter_free(and->sub[0]);
    filter_free(and->sub[1]);
    free(f);
}

struct filter *filter_and(struct filter *a, struct filter *b)
{
    struct filter_and *and = malloc(sizeof(*and));
    and->sub[0] = a;
    and->sub[1] = b;
    and->filter.match = method_match_and;
    and->filter.free = method_free_and;
    return &and->filter;
}
~~~

这样我们的AND操作可以结合一个正则表达式匹配器和一个glob匹配器、或两个正则表达式匹配器，甚至是其他的AND操作。

为了使我们的作为组件的匹配器更容易使用，我们将创建两个“常量”匹配器。

~~~c
static bool
method_match_and(struct filter *f, const char *string)
{
    return true;
}

static bool
method_match_none(struct filter *f, const char *string)
{
    return false;
}

static void
method_free_noop(struct filter *f)
{
}

struct filter FILTER_ANY  = { method_match_any,  method_free_noop };
struct filter FILTER_NONE = { method_match_none, method_free_noop };
~~~

下面是一个将多个glob匹配器合成成一个匹配器的例子，每一个匹配器的模式串即是程序的一个参数。

~~~c
int main(int argc, char **argv)
{
    struct filter *filter = &FILTER_ANY;
    for (char **p = argv+1; *p; p++)
        filter = filter_and(filter_glob_create(*p), filter);
    pass_match(stdin, stdout, filter);
    filter_free(filter);
    return 0;
}
~~~

注意到我们只需要调用一次`filter_free()`就可以释放所有filter。

多重继承
=======

在前文中，我们提到为了使用类型双关技巧，我们的父类型结构体必须作为子类型结构体的第一个成员。但这样，我们就无法实现多重继承。

不过幸运的是，我们可以推广我们的类型双关技巧，使“必须为第一个成员”这一条件不再是必须的。我们通过使用`container_of`宏来实现这一目的。

~~~c
#include <stddef.h>

#define container_of(ptr, type, member) \
    ((type *)((char *)(ptr) - offsetof(type, member)))
~~~

只要给定一个指向结构体成员的指针，我们的`container_of`宏就能返回只想其所在结构体的指针。假设我们之前定义的正则表达式结构体略有不同，`regex_t`成员成为了第一个成员。

~~~c
struct filter_regex {
    regex_t regex;
    struct filter filter;
}
~~~

我们的构造函数不变，但方法中的类型转换将变为宏调用。

~~~c
static bool
method_match_regex(struct filter *f, const char *string)
{
    struct filter_regex *regex = container_of(f, struct filter_regex, filter);
    return regexec(&regex->regex, string, 0, NULL, 0) == 0;
}

static void
method_free_regex(struct filter *f)
{
    struct filter_regex *regex = container_of(f, struct filter_regex, filter);
    regfree(&regex->regex);
    free(f);
}
~~~

该宏会在编译时被计算好，所以不会影响性能。而且，通过这个宏，我们就能实现多重继承了。