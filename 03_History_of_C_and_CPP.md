## 1. C

C and C++ have always aimed to keep old code working while trying to add new things.

C first appeared in 1970 and was standardized in 1989, giving us the classic C89 and C90. By then, it had mostly taken its current basic form and had a standard library.

C95 added wide characters. C99 is what we now think of as modern C. It added comments, allowed variables to be defined anywhere, and added arrays whose length is decided at runtime, a Boolean type, and `xxx`.

C11 in 2011 added concurrency and atomic operations because CPUs were entering the multicore era. Then came C17 and C23, with binary integers, digit separators, and a real `nullptr`, so `NULL` was no longer needed.

## 2. C++

Although C++ is called C with classes, it is not fully the same as C. Do not write C++ as if it were C. This is allowed in some cases, but it is bad and cumbersome.

The first standard was C++98. It already had classes, containers, templates, exceptions, operator overloading, constructors, and destructors. C++03 then fixed some problems.

C++11 was basically the start of modern C++. It added `auto`, range-based `for`, lambdas, move semantics, smart pointers, and `nullptr`. About `nullptr`: in most cases it is zero. The operating system keeps the program's low addresses unused, so dereferencing it causes a page fault. The operating system can then close or pause the program.

C++11 also added `constexpr` for compile-time calculation, along with standard library threads and locks. C++14 made some fixes and improvements.

C++17 added more modern features, such as structured bindings, improvements to template programming, `xxx`, the type-safe `variant`, `any`, `string_view`, and a standard library file system.

C++20 brought template constraints and coroutines, which were very important updates. There were also package management tools and three-way expressions. Then C++23 brought `xxx`, similar to `xxx` or `xxx`, but better.

C++ also has something called `tuple`, which can return structures. Speaking of old design burdens, look up the Y2K problem. Years were stored using only two digits, and the year 00 was coming. This led to a huge cost in updating and changing old code.
