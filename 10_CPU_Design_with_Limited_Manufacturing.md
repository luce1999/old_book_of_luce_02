## 1. Goals and instruction sets

If a country's manufacturing process is behind, what should it consider when designing a CPU? The most important thing is to set a clear goal. Do not try to compete with mainstream commercial CPUs.

First, make sure programs perform well. Do not give priority to an architecture like Intel's, with a heavy burden from the past. Consider something like RISC, with simpler instructions and architecture. I think compatibility with an existing architecture is not really necessary. If there is already money to build a CPU factory, use a new, stable, simple structure and have a team of programmers complete the software ecosystem.

Hyper-Threading, which is too advanced for this situation, can be dropped completely. Reduce the cache to two levels: one for each core and one shared by the cores. There could even be an instruction that lets a program tell the CPU which address to load into the cache.

Branch prediction can also be left out. Let jump instructions carry information about the chance of taking the jump: whether both paths are about equally likely or one is much more likely. They could even tell the CPU what to run early. In other words, software research can make up for hardware limits.

I do not have enough data to judge the ratio of cores to computing units. Large and small cores are also a problem. Designing small cores separately may be difficult. If the small-core code is the same as the large-core code, there may be almost no difference between them. This is troublesome.

## 2. Isolation and the software ecosystem

The MMU should remain. It should at least provide basic hardware isolation, stop ordinary programs from directly causing damage, and strictly separate kernel mode from protected mode. There should at least be batch-processing instructions, as modern Intel CPUs have.

A special development toolkit is also needed so that simple code written by programmers can run on the hardware. Making code in one language run on different machine architectures is not very hard. Modern architecture translation is fairly mature. Source code can also be kept, and development can still use C++.

These designs still barely count as modern CPUs. They can be simplified further if conditions are worse. Consider some MCU designs, closer to early keypad phones. For example, do not distinguish kernel mode from protected mode at all. Run programs in interpreters, which coordinate memory management. External programs become bytecode, while several interpreters are already running on the hardware.

## 3. Graphics and hardware acceleration

Up to this point, the gap from mainstream computers is not very large. One feature of a modern computer is a large graphics card. More precisely, it is a circuit board plugged into another motherboard through PCIe. With weaker manufacturing, a graphics chip can be built into the motherboard. It can be 2D or 3D.

In actual use, the first thing people notice is slow image refresh. Without a 2D processing chip, the CPU must do the work in software, using a lot of CPU time. There are actually not many instructions for the real business work. Modern CPUs often handle many complex extra layers. Software companies value development time more than performance, so frameworks may be stacked on top of frameworks, making things very bloated.

A 2D chip can also produce 3D images. 3D itself stretches and processes many 2D shapes, broadly made of triangles. The main operations are scaling, stretching, moving, rotating, and filling. 3D has more complexity, such as the camera's front-to-back axis deciding whether a triangle is hidden, and mechanisms such as transparency. Rendering usually does not happen immediately; there is a queue. The GPU itself has many cores and a lot of memory.

Do not plug the video output cable into the motherboard. Plug it into the GPU output. Otherwise, it may not work or may need the CPU to handle it. Graphics has more complex subjects that I will not discuss here.

Overall, use software in place of hardware, choose new and simple architectures first, and provide hardware acceleration. "xxx acceleration" and other acceleration also matter. Video decoding, for example, may be essential. Without it, consider other video formats and use other hardware to process them. Pure CPU decoding will be very slow.

## 4. Compatibility and security

One more point: the biggest attack surface now is the CPU itself, while the motherboard and other peripherals are safe. So a weak CPU may come with powerful other components. The design needs to account for this. Finally, support modern hardware as much as possible.
