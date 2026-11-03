## 1. Initialization and readability

C++ has too many ways to initialize things. It is hard to see directly from the code what the author means, which goes against how humans read. I suggest brace initialization. A more natural approach would state the parameters clearly so readers understand at first glance, instead of using complicated braces, brackets, and other symbols. I will discuss this separately.

This also shows that C++ has too many solutions to the same problem, each with different details. When people do not see what they expect, the mental load becomes large. This is also why people dislike reading other people's C++ code.

C++ has no `print` function. Printing to the console is cumbersome, and the symbols are unclear. They may help in some cases, but other methods can do the same thing. Overall, it is still hard to understand.

## 2. Old design burdens and macros

Next are C++'s old design problems. It largely needs to support old code, even some C-like code. This inevitably makes it cumbersome or gives it several solutions to one problem. C++ is still changing. It is now C++23, but most companies and projects still use older versions such as C++14. I prefer C++17. The latest C++ version is not especially good either. I will discuss its history of changes separately.

The classic "xxx" also reflects the C++ design approach: expose as many details as possible, allow changes, and assume programmers will remember every word and document.

There are also macros. They often fail to do what they should. For the earlier problem, for example, basic wrapping could let users package common functions for easy use. Zero-cost abstraction has no side effects. But the current macro design is a failure and does not achieve the intended result.

The official C++ side should offer a sensible set of functions and other things already processed by macros, so ordinary users can directly use higher-level wrappers. Designers of languages such as Python consider programmers' feelings. They predict possible problems and handle them at the language design level. The C++ side has not done this well.

C++ macros also cause name-replacement pollution. `#define` has never properly isolated different files and libraries. This is a basic language problem, and the resulting bugs are often hidden.

My idea is to keep the main parts of C++, perhaps based on C++17, and design another language related to macros. Daily development can use this macro language. Some C++ code can also be written, but it must be stated separately, like C++ treats asm. The macro language ultimately becomes C++ code, so the compiler does not need changing. This may be the best way to improve the situation now. Of course, one could also mainly write C++ and use macros only in certain areas.

## 3. Style, the standard library, and tools

Line-break style and variable style in C++ are not problems at all. Have the editor force the conversion; the syntax is not affected. Changing variable names can be more troublesome and may introduce errors, so it needs care.

The C++ standard library has a poor naming style. Meanings are unclear and cannot be understood literally. There are historical reasons. Early code took the good names. Later names cannot conflict and must still show their connection to older names. That led to the current approach. I will not go into it here.

Header files are another cumbersome historical problem, creating much repeated code. Other languages do not have this problem, so it is actually easy to solve. Package managers automatically download and manage third-party libraries. I will not discuss them further here.

When C++ code is wrong, editors often fail to point out the obvious error. Instead, they report a problem inside a library or elsewhere, which is almost no help. But this is an editor problem, not a C++ design problem. So for beginners, the editor's ability to understand syntax is actually more important.

The standard library has little content. It lacks JSON, networking, Unicode, file I/O, and so on. Algorithm code is also long. For example, `xxx`, `xxx`, and `xxx`: the first saves `test` as an element when it cannot find it. The latter ignores an existing entry instead of replacing it. This is poor design. Every operation should return success or failure, instead of requiring another `get` to check whether `set` worked, adding extra cost.

## 4. Template programming and exceptions

One strange issue is that the C++ template language was discovered later. People unexpectedly found that it was Turing-complete. I do not know template programming very well either. Its syntax is extremely complex.

One way to understand it is to imagine a variable manager, except that variables only exist before the compilation stage. Another way is to understand that compiling code is not simply translation between similar languages. The two are completely different. Compilation is more like parsing or processing an advanced configuration file. For example, one line in a high-level language asks for ten loop iterations, and compilation produces ten lines of machine instructions. This is not a very accurate example, but it gives the idea.

Never use exceptions in any situation. Stack unwinding is troublesome and causes stuttering. Google gives the same advice.
