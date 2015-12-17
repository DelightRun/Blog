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

# Chapter 9 - Statements

1. Don't declare a variable until you have a value to initialize it with. `section 9.3` `section 9.4.3` `section 9.5.2`
2. Prefer a `switch`-statement to an `if`-statement when there is a choice. `section 9.4.2`
3. Prefer a range-`for`-statement to a `for`-statement when there is a choice. `section 9.5.1`
4. Prefer a `for`-statement to a `while`-statement when there is an obvious loop variable. `section 9.5.2`
5. Prefer a `while`-statement to a `for`-statement when there is no obvious loop variable. `section 9.5.3`
6. Avoid `do`-statements. `section 9.5`
7. Avoid `goto`. `section 9.6`
8. Keep comments crisp.
9. Don't say in comments what can be clearly stated in code. `section 9.7`
10. State intent in comments. `section 9.7`
11. Maintain a consistent indentation style. `section 9.7`

# Chapter 10 - Expressions

1. Prefer the standard library to other libraries and to "handcrafted code". `section 10.2.8`
2. Use character-level input only when you have to. `section 10.2.3`
3. When reading, always consider ill-formed input. `section 10.2.3`4.
4. Prefer suitable abstractions (class, algorithms, etc.) to direct use of language features (e.g. ints, statements). `section 10.2.8`
5. Avoid complicated expressions. `section 10.3.3`
6. If in doubt about operator precedence, parenthesize. `section 10.3.3`
7. Avoid expressions with undefined order of evaluation. `section 10.3.2`
8. Avoid narrowing conversions. `section 10.5.2`
9. Define symbolic constants to avoid "magic constants". `section 10.4.1`
10. Avoid narrowing conversions. `section 10.5.2`

# Chapter 11 - Select Operations

1. Prefer prefix `++` over suffix `++`. `section 11.1.4`
2. Use resource handles to avoid leaks, premature deletion, and double deletion. `section 11.2.1`
3. Don't put objects on the free store if you don't have to, prefer scoped variables. `section 11.2.1`
4. Avoid "naked `new`" and "naked `delete`". `section 11.2.1`
5. Use RAII. `section 11.2.1`
6. Prefer a named function object to a lambda if the operation requires comments. `section 11.4.2`
7. Prefer a named function object to a lambda if the operation is generally useful. `section 11.4.2`
8. Keep lambdas short. `section 11.4.2`
9. For maintainability and correctness, be careful about capture by reference. `section 11.4.3.1`
10. Let the compiler deduce the return type of a lambda. `section 11.4.4`
11. Use the `T{e}` natation for construction. `section 11.5.1`
12. Avoid explicit type conversion (casts). `section 11.5`
13. When explicit type conversion is necessary, prefer a named cast. `section 11.5`
14. Consider using a run-time checked cast, such as `narrow_cast<>()`, for conversion between numeric types. `section 11.5`

# Chapter 12 - Functions

1. "Package" meaningful operations as carefully named function. `section 12.1`
2. A function should perform a single logical operation. `section 12.1`
3. Keep functions short. `section 12.1`
4. Don't return pointers or references to local variables. `section 12.1.4`
5. If a function may have to be evaluated at compile time, declare it `constexpr`. `section 12.1.6`
6. If a function cannot return, mark it `[[noreturn]]`. `section 12.1.7`
7. Use pass-by-value for small objects. `section 12.2.1`
8. Use pass-by-`const`-reference to pass large values that you don't need to modify. `section 12.2.1`
9. Return a result as a `return` value rather than modifying an object through an argument. `section 12.2.1`
10. Use rvalue references to implement move and forwarding. `section 12.2.1`
11. Pass a pointer if "no object" is a valid alternative (and represent "no object" by `nullptr`). `section 12.2.1`
12. Use pass-by-non-`const`-reference only if you have to. `section 12.2.1`
13. Use `const` extensively and consistently. `section 12.2.1`
14. Assume that a `char*` or a `const char*` argument points to a C-style string. `section 12.2.2`
15. Avoid passing arrays as pointers. `section 12.2.2`
16. Pass a homogeneous list of unknown length as an `initializer_list<T>` (or as some other container). `section 12.2.3`
17. Avoid unspecified numbers of arguments (`...`). `section 12.2.4`
18. Use overloading when functions perform conceptually the same task on different types. `section 12.3`
19. When overloading on integers, provide functions to eliminate common ambiguities. `setion 12.3.5`
20. Specify preconditions and postconditions for your functions. `section 12.4`
21. Prefer function objects (including lambdas) adn virtual functions to pointers to functions. `section 12.5`
22. Avoid macros. `section 12.6`
23. If you must use macros, use ugly names with lots of capital letters. `section 12.6`

# Chapter 13 - Exception Handling

1. Develop an error-handling strategy early in a design. `section 13.1`
2. Throw an exception to indicate that you cannot perform an assigned task. `section 13.1.1`
3. Use exceptions for error handling. `section 13.1.4.2`
4. Use purpose-designed user-defined types as exceptions (not built-in types). `section 13.1.1`
5. If you for some reason cannot use exceptions, mimic them. `section 13.1.5`
6. Use hierarchical error handling. `section 13.1.6`
7. Keep the individual parts of error handling simple. `section 13.1.6`
8. Don't try to catch every exception in every function. `section 13.1.6`
9. Always provide the basic guarantee. `section 13.2` `section 13.6`
10. Provide the strong guarantee unless there is a reason not to. `section 13.2` `section 13.6`
11. Let a constructor establish an invariant, ant throw if it cannot. `section 13.2`
12. Release locally owned resources before throwing an exception. `section 13.2`
13. Be sure that every resource acquired in a constructor is released when throwing an exception in that constructor. `section 13.3`
14. Don't use exceptions where more local control structures will suffice. `section 13.1.4`
15. Use the "Resource Acquisition Is Initialization" and exception handlers to maintain invariant. `section 13.5.2.2`
16. Minimize the use of `try`-blocks. `section 13.3`
17. Not every program needs to be exception-safe. `section 13.1`
18. Use "Resource Acquisition Is Initialization" and exception handlers to maintain invariants. `section 13.5.2.2`
19. Prefer proper resource handles to the less structured `finally`. `section 13.3.1`
20. Design your error-handling strategy around invariants. `section 13.4`
21. What can be checked at compile time is usually best checked at compile time (using `static_assert`). `section 13.4`
22. Design your error-handling strategy to allow for different levels of checking/enforcement. `section 13.4`
23. If your function may not throw, declare it `noexcept`. `section 13.5.1.1`
24. Don't use exception specification. `section 13.5.1.3`
25. Catch exceptions taht may be part of a hierarchy by reference. `section 13.5.2`
26. Don't assume that every exception is derived from class `exception`. `section 13.5.2.2`
27. Have `main()` catch and report all exceptions. `section 13.5.2.2` `section 13.5.2.4`
28. Don't destroy information before you have its replacement ready. `section 13.6`
29. Leave operands in valid states before throwing an exception from an assignment. `section 13.2`
30. Never let an exception escape from a destructor. `section 13.2`
31. Keep ordinary code and error-handling code separate. `section 13.1.1` `section 13.1.4.2`
32. Beware of memory leaks caused by memory allocated by `new` not being released in case of an exception. `section 13.3`
33. Assume that every exception that can be thrown by a function will be thrown. `section 13.2`
34. A library shouldn't unilaterally terminate a program. Instead, throw an exception and let a caller decided. `section 13.4`
35. A library shouldn't produce diagnostic output aimed at an end user. Instead, throw an exception and let a caller decide. `section 13.1.3`

# Chapter 14 - Namespaces

1. Use namespaces to express logical structure. `section 14.3.1`
2. Place every nonlocal name, except main(), in some namespace. `section 14.3.1`
3. Design a namespace so that you can conveniently use it without accidentally gaining access to unrelated namespaces. `section 14.3.3`
4. Avoid very short names for namespaces. `section 14.4.2`
5. If necessary, use namespace aliases to abbreviate long namespace names. `section 14.4.2`
6. Avoid placing heavy notational burdens on users of your namespaces. `section 14.2.2` `section 14.2.3`
7. Use separate namespaces for interfaces and implementations. `section 14.3.3`
8. Use the `Namespace::member` notation when defining namespace members. `section 14.4`
9. Use `inline` namespaces to support versioning. `section 14.4.6`
10. Use `using`-directives for transition, for foundational libraries (such as `std`), or within a local scope. `section 14.4.9`
11. Don't put a `using`-directive in a header file. `section 14.2.3`

# Chapter 15 - Source Files and Programs

1. Use header files to represent interfaces and to emphasize logical structure. `section 15.1` `section 15.3.2`
2. `#include` a header in the source file that implements its functions. `section 15.3.1`
3. Don't define global entities with the same name and similar-but-different meanings in different translation units. `section 15.2`
4. Avoid non-inline function definitions in headers. `section 15.2.2`
5. USe `#include` only at global scope and in namespaces. `section 15.2.2`
6. `#include` only complete declarations. `section 15.2.2`
7. Use include guards. `section 15.3.3`
8. `#include` C headers in namespaces to avoid global names. `section 14.4.9` `section 15.2.4`
9. Make headers self-contained. `section 15.2.3`
10. Distinguish between users' interfaces and implementers' interfaces. `section 15.3.2`
11. Distinguish between average users' interfaces and expert users' interfaces. `section 15.3.2`
12. Avoid nonlocal objects that require run-time initialization in code intended for use as part of non-C++ programs. `section 15.4.1`

# Chapter 16 - Classes

1. Represent concepts as classes. `section 16.1`
2. Separate the interface of a class from its implementation. `section 16.1`
3. Use public data (`struct`s) only when it really is just data an no invariant is meaningful for the data members. `section 16.2.4`
4. Define a constructor to handle initialization of objects. `section 16.2.5`
5. By default declare single-argument constructors `explicit`. `section 16.2.6`
6. Declare a member function that does not modify the state of its object `const`. `section 16.2.9`
7. A concrete type is the simplest kind of class. Where applicable, prefer a concrete type over more complicated classes and over plain data structures. `section 16.3`
8. Make a function a member only if it needs direct access to the representation of a class. `section 16.3.2`
9. Use a namespace to make the association between a class and its helper functions explicit. `section 16.3.2`
10. Make a member function that doesn't modify the value of its object a `const` member function. `section 16.2.9.1`
11. Make a function that needs access to the representation of a class but needn't be called for a specific object a `static` member function. `section 16.2.12`

# Chapter 17 - Construction, Cleanup, Copy, and Move

1. Design constructors, assignments, and the destructor as a matched set of operations. `section 17.1`
2. Use a constructor to establish an invariant for a class. `section 17.2.1`
3. If a constructor acquires a resource, its class needs a destructor to release the resource. `section 17.2.2`
4. If a class has a virtual function, it needs a virtual destructor. `section 17.2.5`
5. If a class does not have a constructor, it can be initialized by memberwise initialization. `section 17.3.1`
6. Prefer `{}` initialization over `=` and `()` initialization. `section 17.3.2`
7. Give a class a default constructor if and only if there is a "natural" default value. `section 17.3.3`
8. If a class is a container, give it an initializer-list construtor. `section 17.3.4`
9. Initialize members and bases in their order of declaration. `section 17.4.1`
10. If a class has a reference member, it probably needs copy operations (copy constructor and copy assignment). `section 17.4.1.1`
11. Prefer member initialization over assignment in a constructor. `section 17.4.1.1`
12. Use in-class initializers to provie default values. `section 17.4.4`
13. If a class is a resource handle, it probably needs copy and move operations. `section 17.5`
14. When writing a copy constructor, be careful to copy every element that needs to be copied (beware of default initializers). `section 17.5.1.1`
15. A copy operations should provide equivalence and independence. `section 17.5.1.3`
16. Beware of entangled data structures. `section 17.5.1.1`
17. Prefer move semantics and copy-on-write to shallow copy. `section 17.5.1.3`
18. If a class is used as a base class, protect against slicing. `section 17.5.1.4`
19. If a class needs a copy operation or a destructor, it probably needs a constructor, a destructor, a copy assignment, and a copy constructor. `section 17.6`
20. If a class has a pointer member, it probably needs a destructor and non-default copy operations. `section 17.6.3.3`
21. If a class is a resource handle, it needs a constructor, a destructor, and non-default copy operations. `section 17.6.3.3`
22. If a default constructor, assignment, or destructor is appropriate, let the compiler generate it (don't rewrite it yourself). `section 17.6`
23. Be explicit about your invariants, use constructors to establish them and assignments to maintain them. `section 17.6.3.2`
24. Make sure that copy assignments are safe for self-assignment. `section 17.5.1`
25. When adding a new member to a class, check to see if there are user-defined constructors that need to be updated to initialize the member. `section 17.5.1`

# Chapter 18 - Operator Overloading

1. Define operators primarily to mimic conventional usage. `section 18.1`
2. Redefine or prohibit copying if the default is not appropriate for a type. `section 18.2.2`
3. For large operands, use `const` reference argument types. `section 18.2.4`
4. For large results, use a move constructor. `section 18.2.4`
5. Prefer member functions over nonmembers for operations that need access to the representation. `section 18.3.1`
6. Prefer nonmember functions over members for operations that do not need access to the representation. `section 18.3.2`
7. Use namespaces to associate helper functions with "their" class. `section 18.2.5`
8. Use nonmember functions for symetric operators. `section 18.3.2`
9. Use member functions to express operators that require an lvalue as their left-hand operand. `section 18.3.3.1`
10. Use user-defined literals to mimic conventional notation. `section 18.3.4`
11. Provide "`set()` and `get()` functions" for a data member only if the fundamental semantics of a class require them. `section 18.3.5`
12. Be cautious about introducing implicit conversions. `section 18.4`
13. Avoid value-destroying ("narrowing") conversions. `section 18.4.1`
14. Do not define the same conversion as both a constructor and a conversion operator. `section 18.4.3`

# Chapter 19 - Friends and Members

1. Use `operator[]()` for subscripting and for selection based on a single value. `section 19.2.1`
2. Use `operator()()` for call semantics, for subscripting, and for selection based on multiple values. `section 19.2.2`
3. Use `operator->()` to dereference "smart pointers". `section 19.2.3`
4. Prefer prefix `++` over suffix `++`. `section 19.2.4`
5. Define the global `operator new()` and `operator delete()` only if you really have to. `section 19.2.5`
6. Define member `operator new()` and member `operator delete()` to control allocation and deallocation of objects of a specific class or hierarchy of classes. `section 19.2.5`
7. Use user-defined literals to mimic conventional notation. `section 19.2.6`
8. Place literal operators in separate namespaces to allow selective user. `section 19.2.6`
9. For nonspecialized uses, prefer the standard `string` to the result of your own exercises. `section 19.3`
10. Use a friend function if you need a nonmember function to have access to the representation of a class (e.g. to improve notation or to access the representation of two classes). `section 19.4`
11. Prefer member functions to friend functions for granting access to the implementation of a class. `section 19.4.2`

# Chapter 20 - Derived Classes

1. Avoid type fields. `section 20.3.1`
2. Access polymorphic objects through pointers and references. `section 20.3.2`
3. Use abstract classes to focus design on the provision of clean interfaces. `section 20.4`
4. Use `override` to make overriding explicit in large class hierarchies. `section 20.3.4.1`
5. Use `final` only sparingly. `section 20.3.4.2`
6. Use abstract classes to specify interfaces. `section 20.4`
7. Use abstarct classes to keep implementation details out of interfaces. `section 20.4`
8. A class with a virtual function should have a virtual destructor. `section 20.4`
9. An abstract class typically doesn't need a constructor. `section 20.4`
10. Prefer `private` members for implementation details. `section 20.5`
11. Prefer `public` members for interfaces. `section 20.5`
12. Use `protected` members only carefully when really needed. `section 20.5.1.1`
13. Don't declare data members `protected`. `section 20.5.1.1`

# Chapter 21 - Class Hierarchies

1. Use `unique_ptr` or `shared_ptr` to avoid forgetting to `delete` objects created using `new`. `section 21.2.1`
2. Avoid data members in base classes intended as interfaces. `section 21.2.1.1`
3. Use abstract classes to express interfaces. `section 21.2.2`
4. Give an abstract class a virtual destructor to ensure proper cleanup. `section 21.2.2`
5. Use `override` to make overriding explicit in large class hierarchies. `section 21.2.2`
6. Use abstract classes to support interface inheritance. `section 21.2.2`
7. Use base classes with data members to support implementation inheritance. `section 21.2.2`
8. Use ordinary multiple inheritance to express a union of features. `section 21.3`
9. Use multiple inheritance to separate implementation from interface. `section 21.3`
10 Use a virtual base to represent something common to some, but not all, classes in a hierarchy. `section 21.3.5`

# Chapter 22 - Run-Time Type Information

1. Use virtual functions to ensure that the same operation is performed independently of which interface is used for an object. `section 22.1`
2. Use `dynamic_cast` where class hierarchy navigation is unavoidable. `section 22.2`
3. Use `dynamic_cast` for type-safe explicit navigation of a class hierarchy. `section 22.2.1`
4. Use `dynamic_cast` to a reference type when failure to find the required class is considered a failure. `section 22.2.1.1`
5. Use `dynamic_cast` to a pointer type when failure to find the required class is considered a valid alternative. `section 22.2.1.1`
6. Use double dispatch or the visitor pattern to express operations on two dynamic types (unless you need an optimized lookup). `section 22.3.1`
7. Don't call virtual functions during construction or destruction. `section 22.4`
8. Use `typeid` to implement extended type information. `section 22.5.1`
9. Use `typeid` to find the type of an object (and not to find an interface to an object). `section 22.5`
10. Prefer virtual functions to repeated `switch`-statements based on `typeid` or `dynamic_cast`. `section 22.6`

# Chapter 23 - Templates

1. Use templates to express algorithms that apply to many argument types. `section 23.1`
2. Use templates to express containers. `section 23.2`
3. Note that `template<class T>` and `template<typename T>` are synonymous. `section 23.2`
4. When defining a template, first design and debug a non-template version, later generatlize by adding parameters. `section 23.2.1`
5. Templates are type-safe, but checking happens too late. `section 23.3`
6. When designing a template, carefully consider the concepts (requirements) assumed for its template arguments. `section 23.3`
7. If a class template should be copyable, give it a non-template copy constructor and a non-template copy assignment. `section 23.4.6.1`
8. If a class template should be movable, give it a non-template move constructor and a non-template move assignment. `section 23.4.6.1`
9. A virtual function member cannot be a template member function. `section 23.4.6.2`
10. Define a type as a member of a template only if it depends on all the class template's arguments. `section 23.4.6.3`
11. Use function templates to deduce class template argument types. `section 23.5.1`
12. Overload function templates to get the same semantics for a variety of argument types. `section 23.5.3`
13. Use argument substitution failure to provide just the right set of functions for a program. `section 23.5.3.2`
14. Use teplate aliases to simplify notation and hide implementation details. `section 23.6`
15. There is no separate compilation of templates: `#include` template definitions in every translation unit that uses them. `section 23.7`
16. Use ordinary functions as interfaces to code that cannot deal with templates. `section 23.7.1`
17. Separately compile large templates and templates with nontrivial context dependencies. `section 23.7`

# Chapter 24 - Generic Programming

1. A template can pass argument types without loss of information. `section 24.1`
2. Templates provide a general mechanism for compile-time programming. `section 24.1`
3. Templates provide compile-time "duck typing". `section 24.1`
4. Design generic algorithms by "lifting" from concrete examples. `section 24.2`
5. Generalize algorithms by specifying template argument requirements in terms of concepts. `section 24.3`
6. Do not give unconventional meaning to conventional notation. `section 24.3`
7. Use concepts as a design tool. `section 24.3`
8. Aim for "plug comatibility" among algorithms and argument type by using common and regular template argument requirements. `section 24.3`
9. Discover a concept by minimizing an algorithm's requirements on its template arguments and then generalizing for wider use. `section 24.3.1`
10. A concept is not just a description of the needs of a particular implementation of an algorithm. `section 24.3.1`
11. If possible, choose a concept from a list of well-known concepts. `section 24.3.1` `section 24.4.4`
12. The default concept for a template argument is `Regular`. `section 24.3.1`
13. Not all template argument types are `Regular`. `section 24.3.1`
14. A concept requires a semantic aspect, it is not primarily a syntactic notion. `section 24.3.1` `section 24.3.2`
15. Make concepts concrete in code. `section 24.4`
16. Express concepts as compile-time predicates (`constexpr` functions) and test them using `static_assert()` or `enable_if<>`. `section 24.4`
17. Use axioms as a design tool. `section 24.4.1`
18. Use axioms as a guide for testing. `section 24.4.1`
19. Some concepts involve two or more template arguments. `section 24.4.2`
20. Concepts are not just types of types. `section 24.4.2`
21. Concepts can involve numeric values. `section 24.4.3`
22. Use concepts as a guide for testing template definitions. `section 24.4.5`

# Chapter 25 - Specialization

1. Use templates to improve type safety. `section 25.1`
2. Use templates to raise the level of abstraction of code. `section 25.1`
3. Use templates to provide flexible and efficient parameterization of types and algorithms. `section 25.1`
4. Remember that value template arguments must be compile-time constants. `section 25.2.2`
5. Use function objects as type arguments to parameterize types and algorithms with "policies". `section 25.2.3`
6. Use default template arguments to provide simple notation for simple uses. `section 25.2.5`
7. Specialize templates for irregular types (such as arrays). `section 25.3`
8. Specialize templates to optimize for important cases. `section 25.3`
9. Define the primary template before any specialization. `section 25.3.1.1`
10. A specialization must be in scope for every use. `section 25.3.1.1`
