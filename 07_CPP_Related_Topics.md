## 1. Windows and addresses

How does Windows start an EXE? Redirecting function addresses mainly reduces the risk of simple virus attacks. Some early attacks mainly relied on reverse engineering a program and then finding its problems.

## 2. Bit widths and type names

A byte is 8 bits, a word is 16 bits, a dword is 32 bits, and a qword is 64 bits. Why is a byte 8 bits? There is no special reason. Nothing in the CPU directly corresponds to the name byte. It is mainly because early CPU registers were 8 bits wide. The name word came later with 16-bit CPUs. The names themselves have no special meaning.

Mainstream CPUs are 64-bit now, but actual memory addresses may use only 48 bits, 52 bits, or another width. Larger address spaces are not needed and may also cause problems with motherboard wiring.

Windows has some custom types. For example, Handle, commonly used in the Windows API, is 64-bit.

The C++ types `int` and `long` often behave differently across platforms. The types include `short`, `int`, `long`, and `long long`. What an ugly name `long long` is. Did a human name it? Anyway, each type is always larger than the one before it.

`bool` can sometimes be 8 bits. There are actually more types, such as `char` and `wchar`.
