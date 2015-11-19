---
layout: post
title: "TC++PL Advices"
date: 2015-11-16 16:25:23 +0800
comments: true
categories: [C++, TC++PL]
---

Advices from *The C++ Programming Language, 4th Edition*.

<!-- more -->

# Chapter 2 - A Tour of C++: The Basics

1. Don't panic! All will become clear in time. `section 2.1`
2. You don't have to know every detail of C++ to write good programs. `section 1.3.1`
3. Focus on programming techniques, not on language features. `section 2.1`

# Chapter 3 - A Tour of C++: Abstraction Mechanisms

1. Express ideas directly in code. `section 3.2`
2. Define classes to represent application concepts directly in code. `section 3.2`
3. Use concrete classes to represent simple concepts and performance-critical components. `section 3.2.1`
4. Avoid "naked" `new` and `delete` operations. `section 3.2.1.2`
5. Use resource handles and RAII to manage resources. `section 3.2.2`
6. Use abstract classes as interfaces when complete separation of interface and implementation is needed. `section 3.2.2`
7. Use class hierarchies to represent concepts with inherent hierarchical structure. `section 3.2.4`
8. When designing a class hierarchy, distinguish between implementation inheritance and interface inheritance. `section 3.2.4`
9. Control construction, copy, move, and destruction of objects. `section 3.3`
10. Return containers by value (relying on move for efficiency). `section 3.3.2`
11. Provide strong resource safety: that is, never leak anything that you think of as a resource. `section 3.3.3`
12. Use container, defined as resource handle templates, to hold collections of values of the same type. `section 3.4.1`
13. Use function templates to represent general algorithms. `section 3.4.2`
14. Use function objects, including lambdas, to represent policies and actions. `section 3.4.3`
15. Use type and template aliases to provide a uniform notation for types that may vary among similar types or among implementations. `section 3.4.5`

# Chapter 4 - A Tour of C++: Containers and Algorithms

1. Don't reinvent the wheel, use libraries. `section 4.1`
2. When you have a choices, prefer the standard library over other libraries. `section 4.1`
3. Do not think that the standard library is ideal for everything. `section 4.1`
4. Remember to `#include` the headers for the facilities you use. `section 4.1.2`
5. Remember that standard-library facilities are defined in namespace `std`. `section 4.1.2`
7. Prefer `strings`s over C-style strings (a `char *`). `section 4.2` `section 4.3.2`
8. Prefer `vector<T>`, `map<K,T>`, and `unordered_map<K,T>` over `T[]`. `section 4.4`
9. Know your standard containers and their tradeoffs. `section 4.4`
10. Use `vector` as your default container. `section 4.4.1`
11. Prefer compact data structures. `section 4.4.1.1`
12. If in doubt, use a range-checked vector. `section 4.4.1.2`
13. Use `push_back()` or `back_inserter()` to add elements to a container. `section 4.4.1` `section 4.5`
14. Use `push_back()` on a `vector` rather than `realloc()` on an array. `section 4.5`
15. Catch common exceptions in `main()`. `section 4.4.1.2`
16. Know your standard algorithms and prefer them over handwritten loops. `section 4.5.5`
17. If iterator use gets tedious, define container algorithms. `section 4.5.6`

# Chapter 5 - A Tour of C++: Concurrency and Utilities

1. Use resource handles to manage resources (RAII). `section 5.2`
2. Use `unique_ptr` to refer to objects of polymorphic type. `section 5.2.1`
3. Use `shared_ptr` to refer to shared objects. `section 5.2.1`
4. Use type-safe mechanisms for concurrency. `section 5.3`
5. Minimize the use of shared data. `section 5.3.4`
6. Don't choose shared data for communication because of "efficiency" without thought and preferably not without measurement. `section 5.3.4`
7. Think in terms of concurrent tasks, rather than threads. `section 5.3.5`
8. A library doesn't have to be large or complicated to be useful. `section 5.4`
9. Time your programs before making claims about efficiency. `section 5.4.1`
10. You can write code to explicitly depend on properties of types. `section 5.4.2`
11. Use regular expressions for simple pattern matching. `section 5.5`
12. Don't try to do serious numeric computation using only the language, use libraries. `section 5.6`
13. Properties of numeric types are accessible through `numeric_limits`. `section 5.6.5`

# Chapter 6 - Types and Declarations

1. For the final word on language definition issues, see the ISO C++ standard. `section 6.1`
2. Avoid unspecified and undefined behavior. `section 6.1`
3. Isolate code that must depend on implementation-defined behavior. `section 6.1`
4. Avoid unnecessary assumptions about the numeric value of characters. `section 6.2.3.2` `section 10.5.2.1`
5. Remember that an integer starting with a `0` is octal. `section 6.2.4.1`
6. Avoid "magic constants". `section 6.2.4.1`
7. Avoid unnecessary assumptions about the size of integers. `section 6.2.8`
8. Avoid unnecessary assumptions about the range and precision of floating-point types. `section 6.2.8`
9. Prefer plain `char` over `signed char` and `unsigned char`. `section 6.2.3.1`
10. Beware of conversions between signed and unsigned types. `section 6.2.3.1`
11. Declare one name (only) per declaration. `section 6.3.2`
12. Keep common and local names short, and keep uncommon and nonlocal names longer. `seciont 6.3.3`
13. Avoid similar-looking names. `section 6.3.3`
14. Name an object to reflect its meaning rather than its type. `section 6.3.3`
15. Maintain a consistent naming style. `section 6.3.3`
16. Avoid `ALL_CAPS` names. `section 6.3.3`
17. Keep scopes small. `section 6.3.4`
18. Don't use the same name in both a scope and an enclosing scope. `section 6.3.4`
19. Perfer the `{}`-initializer syntax for declarations with a named type. `section 6.3.5`
20. Perfer thr `=` syntax for the initialization in declarations using `auto`. `section 6.3.5`
21. Avoid uninitialized variables. `section 6.3.5.1`
22. Use an alias to define a meaningful name for a built-in type in cases in which the built-in type used to represent a value might change. `section 6.5`
23. Use an alias to define synonyms for types, use enumerations and classes to define new types. `section 6.5`

# Chapter 7 - Pointers, Arrays, and References

1. Keep use of pointers simple and straightforward. `section 7.4.1`
2. Avoid nontrivial pointer arithmetic. `section 7.4`
3. Take care not to write beyond the bounds of an array. `section 7.4.1`
4. Avoid multidimensional arrays, define suitable containers instead. `section 7.4.2`
5. Use `nullptr` rather than `0` or `NULL`. `section 7.2.2`
6. Use containers (e.g. `vector`, `array` and `valarray`) rather than built-in (C-style) arrays. `section 7.4.1`
7. Use `string` rather than zero-terminated arrays of `char`. `section 7.4`
8. Use raw strings for string literals with complicated uses of backslash. `section 7.3.2.1`
9. Prefer `const` reference arguments to plain reference arguments. `section 7.7.3`
10. Use rvalue references (only) for forwarding and move semantics. `section 7.7.2`
11. Keep pointers that represent ownership inside handle classes. `section 7.6`
12. Avoid `void*` except in low-level code. `section 7.2.1`
13. Use `const` pointers and `const` references to express immutablility in interfaces. `section 7.5`
14. Prefer references to pointers as arguments, except where "no object" is a reasonable option. `section 7.7.4`

# Chapter 8 - Structures, Unions, and Enumerations

1. When compactness of data is important, lay out structure data members with larger members before smaller ones. `section 8.2.1`
2. Use bit-fields to represent hardware-imposed data layouts. `section 8.2.7`
3. Don't naively try to optimize memory consumption by packing several values into a single byte. `section 8.2.7`
4. Use `union`s to save space (represent alternatives) and never for type conversion. `section 8.3`
5. Use enumerations to represent sets of named constants. `section 8.4`
6. Prefer `class enum`s over "plain" `enum`s to minimize surprises. `section 8.4`
7. Define operations on enumerations for safe and simple use. `section 8.4.1`
