---
layout: post
title: "Modern C++ Design Example(1) -- Policy"
date: 2015-11-10 19:17:45 +0800
comments: true
categories: Programming, C++
---

Example of *Modern C++ Design* Chapter 1 -- Policy

<!-- more -->

# Define Some Policy

```cpp
template <class T>
class OpNewCreator
{
    static T* Create()
    {
        return new T;
    }
protected:
    ~OpNewCreator() {}
};

template <class T>
struct MallocCreator
{
    static T* Create()
    {
        void* buf = std::malloc(sizeof(T));
        if (!buf) return 0;
        return new(buf) T;
    }
protected:
    ~MallocCreator() {}
};

template <class T>
struct PrototypeCreator
{
    PrototypeCreator(T* pObj = 0)
        :pPrototype_(pObj)
    {}
    T* Create()
    {
        return pPrototype_ ? pPrototype_->Clone() : 0;
    }
    T* GetPrototype() { return pPrototype_; }
    void SetPrototype(T* pPrototype_ = pObj; )
private:
    T* pPrototype_;
protected:
    ~PrototypeCreator() {}
};
```

# Create Host Class

```cpp
// Library Code
template <template <class> class CreationPolicy>
class WidgetManager : public CreationPolicy<Widget>
{
    ...
};
```

And now we can use our host class like this:

```cpp
// Application Code
typedef WidgetManager<OpNewCreator> MyWidgetMgr;
// Or
using MyWidgetMgr = WidgetManager<OpNewCreator>;
```

# Add Extra Function To Host Class

```cpp
// Library Code
template <template <class> class CreationPolicy>
class WdigetManager : public CreationPolicy<Widget>
{
    ...
    void SwitchPrototype(Widget* pNewPrototype)
    {
        CreationPolicy<Widget>& myPolicy = *this;
        delete myPolicy.GetPrototype();
        myPolicy.SetPrototype(pNewPrototype);
    }
};
```

The resulting context is:

+ If the user instantiates `WidgetManager` with a Creator policy class that 
supports prototypes, she can use `SwitchPrototype`.

+ If the user instantiates `WidgetManager` with a Creator policy class that 
does not support prototypes and tries to use `SwitchPrototype`, 
a compile-time error occurs.

+ If the user instantiates `WidgetManager` with a Creator policy class that 
does not support prototypes and does not try to use `SwitchPrototype`, 
the program is valid.
