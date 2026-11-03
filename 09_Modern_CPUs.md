## 1. Instruction execution and microarchitecture

The main feature of modern CPUs is that they improve their internal design as much as possible without changing the instruction set. Whatever happens inside, the external interface stays stable. Some of the following comes from documents, and some is guesswork. It does not describe every CPU, and may not help much with writing code. I will discuss CPU-friendly code separately. Here we mainly discuss Intel's x86 series.

First, consider the CPU's workflow: fetch, decode, execute, and write back. Fetching means getting an instruction, usually from the L1 cache. If it is not there, a cache miss occurs and it is fetched from memory. Decoding turns instructions into the CPU's internal instructions, or microcode. This involves register renaming. The registers actually used may differ from those named in the instruction. The CPU checks whether they are related.

Execution is done by specific computing units. Several units may work at once, so the CPU must schedule them internally. Next comes write-back. More precisely, the write-back order is uncertain, and the target may only be a cache, not memory. A core gives the task to the CPU's internal management system, which writes it back and informs other CPUs.

CPUs also predict branches, processing some instructions early, especially when it is unclear whether a JMP will jump. If the prediction fails, the result is not written. Whatever happens inside, the CPU follows its external interface, improving efficiency while staying correct. Internal CPU instructions are a deep subject.

## 2. Caches, cores, and memory protection

A CPU usually has three cache levels. L1 is the smallest, and L2 is a little larger. Each core has these two levels. L3 is shared by the whole CPU and mainly gets data from memory. The memory controller, or northbridge, is also inside the CPU. The closer a cache is to the CPU, the faster and smaller it is. The CPU coordinates this itself, and the caches also have some learning ability. Communication between cores is fairly complex too.

One feature of Intel CPUs is Hyper-Threading. When a core is working for one thread and has some free capacity, it can do a little work for another thread. This is complex, but can improve performance by about 20%, while adding much more complexity. Programs and the operating system cannot sense it at all.

Another important modern CPU structure is the MMU, which maps virtual addresses. This part can also be called the TLB. It lets several programs use the same code, isolates threads, and adds a xxx layer to the address space. The operating system controls the translation table. Even if a program knows a real physical address or a virtual address in another program, it cannot access it directly. Trying to access a protected address causes a page fault, bringing in the operating system. The MMU can also have cache misses. Performance is better when the cache is valid.

## 3. System calls, concurrency, and interrupts

A system call, or syscall, first puts data agreed on with the operating system into registers. It then runs the syscall instruction and enters the interrupt vector table. The context is saved, and operating system code handles the request. The program is now in kernel mode, or a fully real machine state. Afterward, the context is restored and sysret returns to protected mode. If the operating system code has a problem, such as an injection attack, the program may gain kernel rights.

Several cores working together create cache consistency problems. For example, several threads may write to the same memory area. Modern architectures provide atomic instructions for this. After the work finishes, a write is forced and related CPUs fetch the cache data again. Poor handling can cause serious stuttering.

There is also time slicing. The operating system regularly switches the running program and saves its context. Windows also has APIs for occupying a separate CPU. Processes, threads, and PIDs are not physical concepts. The operating system simulates them. The CPU does not actually know what it is doing. The operating system handles context saving and similar work. The only outside interference a CPU can sense is an interrupt. Interrupts enter the interrupt vector table and can be software or hardware interrupts.

For devices on the motherboard, the CPU also provides DMA. This lets devices move data directly into memory instead of asking the CPU to move it.

## 4. Management systems and instructions

Another special component is xxx. It is a platform that lets Intel control the computer remotely. Its rights are above the operating system and even above machine hardware rights. It cannot be turned off or observed. It is large enough inside to run a small operating system or program. It is inside the CPU, and damaging it would damage the CPU. It can run even when the computer is off, as long as power is connected. There is currently no public, trustworthy information. These systems exist in all CPU versions. Other architectures and makers, such as "xxx," have similar systems. They can control whether a CPU loads an operating system or program. Intel holds the keys. Each device may be different, and the keys may be burned into it. I cannot think of a solution for now. Ordinary programs neither need it nor can call or sense it.

The motherboard BIOS also helps prevent changed or third-party operating systems from loading. This motherboard mechanism can be turned off. It seems that only "xxx" now checks when the OS starts. Management on Intel platforms is not strict.

CPU instructions include addition, division, bit operations, and floating-point operations. One floating-point example is `0.1 + 0.2` producing `0.30000000000000004`. Jump instructions read the Flag register to decide whether to jump. Calculations write states such as carry and overflow into Flag, and jumps read them later.

Some privileged instructions can only be used in kernel mode. Examples involve the hypervisor, kernel-mode registers, and debugging. CS and DS are no longer used, but FS and GS still are. There are also batch calculation instructions called SIMD. They can compare, add, subtract, and so on in batches, reducing the cost of CPU jumps.

The stack can be left completely unused, but "xxx" then needs to be handled manually, which is troublesome. So the stack is a hardware-level speedup, not a requirement. A CPU can also contain other parts, such as graphics chips. These usually cannot be called directly through instructions.

## 5. Radiation, reliability, and cost

One important way to resist radiation in space is three-way voting. The same calculation runs three times, and hardware circuits vote on the result. Space CPUs also use different outer layers and materials. Radiation is divided into ionizing and non-ionizing radiation. One is closer to visible light and radio waves, and the other is nuclear radiation.

The key point about nuclear radiation is that it sends out protons rather than electrons, or positively charged atomic nuclei made of protons and neutrons. Everyday life also has weak radiation, mainly from atoms decaying in matter itself. Large objects are usually hard to accelerate close to light speed. Nuclear fission produces high-energy particles that can damage biological DNA and also flip bits in electronics, changing 0 to 1 or 1 to 0.

Software can run on bare metal, without an operating system, programmed directly for the hardware. There are also many software solutions. For example, error-correcting codes can be recorded for memory data, with regular checks for flipped bits, and data can be backed up. This could be a separate topic.

Home computing chips must also consider cost. CPU design must consider how often each part is damaged during manufacturing and within some time after leaving the factory. This greatly limits the design. For example, if an ALU is easily damaged, a core can have two ALUs but use only one. With only one ALU, its failure may ruin the whole core.

Many CPUs on the market are defective products that have been tested and packaged. They cost less and are marked. For example, "xxx" packages away damaged cores. I do not know whether home CPUs keep checking themselves after leaving the factory; it may depend on the maker. Home CPUs can also suffer bit flips. The probability is low, but not zero. I also wonder whether larger transistors have better radiation resistance.

Software for space-grade CPUs is usually outside the general ecosystem. The design must also consider "xxx," meaning it must never crash. The software is very sensitive to delay and must not spend too long on a time-consuming task.
