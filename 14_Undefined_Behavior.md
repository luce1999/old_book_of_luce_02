## 1. The background of undefined behavior

First, UB, or undefined behavior, is a category deliberately left in the design of a programming language. C++ existed alongside many CPU types with different registers and other data. It had to make room for compilers on different CPUs and let the compiler decide the exact behavior.

Another major issue is the huge C++ ecosystem. It has many compilers, each with its own understanding of C++. Each is powerful, independent, and has a fairly complete ecosystem.

More precisely, with or without UB, and however the compiler compiles, the final machine instructions are fixed. The same code on the same machine gives the same result every time. So in some cases, UB can roughly be understood as a compiler's own preference. Its biggest problem is that programmers do not know some code is UB. The compiler and programmer are not thinking in sync, creating a gap.

## 2. Common examples and risks

The most basic example is an `int` already at its maximum value. Add one, and it enters UB. Most compilers allow wrapping, or seem to do nothing, making it negative. Some compilers report an error. Some programmers may expect it to keep increasing.

The more dangerous part is that, in real development, programmers may not expect the number to reach its maximum and then have one added. This is a common kind of vulnerability. Attackers use it to make a program access their memory or execute an instruction. The best approach is to check first that the result will not wrap, but this costs performance. In some cases wrapping is actually correct. Ultimately, there is a communication barrier between compiler and programmer.

Things such as `xxx` and the number of bytes in an `int` are deliberately left for the compiler to decide. Development needs care about compiler features and the target platform. It is best to state the intended function clearly, for example by using `uint64_t`.

Another classic UB problem is out-of-bounds access. For example, an array has 10 elements, but code tries to access the 11th. Such access is itself legal, and C++ allows it. It may actually be useful, but can easily have disastrous results. A condition check can be added, but costs performance. Address calculation also has problems, which I will not discuss here.

Another case is continuing to access an address through a pointer after that address has been freed. There are also issues involving `new` and `delete`: deleting something not created with `new`, or using `delete` on an array.

## 3. Memory access and code examples

Another special case is accessing an unaligned memory address. Examples include `xxx` and `xxx`.

There is also reading data from an uninitialized variable.

Finally, there are `xxx`, `xxx`, and `xxx`.
