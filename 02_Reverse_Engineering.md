## 1. Preparing the tools and setting the goal

The first step is to prepare the development environment. I suggest installing professional reverse engineering software. Try to find free, powerful tools, and consider having several of them. You also need a debugger, such as `xxx`.

First, what can we see? We can only see the binary code that finally runs on the machine. Here we assume the program is written in C++. Reverse engineering tools are now quite advanced and can usually turn it back into accurate C code. Some programs can be analyzed further, while others cannot. This is a current limit of these tools. In fact, it is also possible to produce C++ code.

Next, decide the goal. Here we assume it is to bypass an existing limit, such as online verification. Basically, find the network-related function and make it return the correct result when called.

Then look for APIs based on that goal. Many programs eventually call Windows APIs, which gives us a starting point. The work involves editing hexadecimal values. Keep the overall program unchanged as far as possible and make only small local changes. Avoid stack problems and handle jumps properly.

You also need a deep understanding of C++ and machine instructions. Without knowing machine instructions, you cannot do this work. You can watch my other videos.

## 2. Program protection and analysis cost

So far, we have discussed xxx programs: `xxx` compiled directly from C++. Now let us discuss code with defensive measures.

First, there may be problems with the symbol table. Data can also be obscured. For example, a whole string may not appear at once; only a small part is compared each time. There is also control flow obfuscation. A program may check something at the start, then run another check later. It may also have fake functions, such as one that is never called but looks "xxx." These measures all increase the cost of analysis.

A more advanced approach turns part of the control flow into bytecode and runs it through an interpreter. This costs little but greatly increases analysis work. The bytecode and interpreter can also be custom-made or include some randomness.

A program can check its environment. It can look for a debugger, or use machine fingerprints to check for a virtual environment, such as xxx. It can also check its own binary to see whether it was changed. However, that checking function can also be disabled.

The program can ask the operating system for help, such as preventing other programs from debugging it. A more advanced method writes to some memory at runtime, then changes its permission from writable to executable to cause more confusion. Network-based methods are also possible.

These are still ordinary programs in protected mode, just with more advanced protection. Reaching kernel mode basically puts a program on the same level as the operating system. Anti-cheat software usually works at this level. It scans memory and disks and also uses online detection.

Denuvo uses xxx encryption, which is more advanced but makes games very slow. This could be a separate topic.

To sum up, programs can often be fully analyzed. The difference is the cost in experience, time, and so on. Rapid client distribution, updates to only part of a client, or different clients for different users can all greatly increase that cost.
