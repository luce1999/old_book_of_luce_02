## 1. Stages of computer development

Computer development can roughly be divided into five stages: electrically and mechanically driven computers around 1940, vacuum tubes around 1950, transistors around 1960, integrated circuits around 1970, and microprocessors.

Up to this point, many problems were still physical, meaning they could be seen and judged with the naked eye. Physical failures were common. Problems mainly remained at the physical level rather than in algorithm design.

Modern computers truly began with integrated circuits. Soviet computers of that time were also of this type. The next step, microprocessors, was very important. Manufacturing improved greatly, and computer architecture was improved or fixed into a set form. One major problem with microprocessors is that the CPU is too fragile and cannot really be repaired or "xxx." Other internal parts cannot be repaired either. This is where computing and electronics engineering really separated.

There is also a stage people often overlook. CPUs tend to bring more parts inside, such as small GPUs and the northbridge, to improve performance. Connections between parts of the computer began to serve the CPU. Only at this stage did the CPU truly gain the highest management position in the computer.

## 2. From mechanical calculation to computing units

The mechanical stage mainly includes devices such as difference engines. I do not know much about their mechanical structure, but they already had the basic shape of a computer: input, output, and computing units. Relay computers are still mechanical computers. They use magnetic force to control switches.

The ability to compute exists naturally in the world, not only in electronic circuits. Looking up trigonometric or exponent tables can count as a kind of computer. A person multiplying numbers on scrap paper can count as one too.

Early computers did not yet have an instruction-level mechanism. Even in the vacuum tube era, changing a program meant changing circuit layouts. To calculate addition, the circuit had to be changed into an adder.

Multiplication acted as a trigger for further development. It first splits data into many calculation tasks and gives them to an adder. The adder's output then becomes new input for further calculation. This makes a controller necessary. Division is harder than addition because the number of steps is not fixed, so the number of runs must be judged. One method starts at one, multiplies that number by the divisor, and checks whether it is greater than the dividend. If not, increase the number, multiply again, and check until it exceeds the dividend, then calculate the remainder. A better method is repeated subtraction, provided there is a subtraction unit.

This involves more complex control flow and comparisons. More precisely, comparison can use subtraction: if subtracting two values gives zero, they are equal. Modern computers still use this method, and there is really no other method. Of course, they also have separate multiplication and division units.

## 3. Registers, memory, and controllers

What was called memory early on could more accurately be seen as a cache for temporary data, closer to registers. Take the division example. Put the dividend in one register, the divisor in B, and the result of multiplying the divisor by a number in C. Keep increasing C and calculating, then put the final result in D. When the controller calls the unit, it puts data in A and B, leaves C to the packaged division unit, and waits for the result in D. This basically completes the packaging of a computing unit.

Next, choose whether to pass parameters through registers or memory. With registers, another computing unit can read D directly and continue, provided the hardware supports it. When the controller tells the packaged division unit to execute, it must say which registers serve which purposes. This is not the same as register renaming.

Memory appeared for several reasons, mainly because adding registers is very expensive. Connecting one computing unit to many registers requires many extra circuits. A better method is to add a memory controller, or a "manager for less-used registers." It moves data from memory into registers or reads it back when needed. This also needs the controller's coordination.

CPU calculation cycles are not as simple as "transistor oscillation." They must avoid conflicts and simultaneous writes and ensure that the right values are read. For example, the next unit must wait until the packaged division unit finishes. The memory controller must also avoid conflicts with registers already in use.

At this point, the computer already has many functions. A simple way for the controller to handle them is to make the controller itself a computing unit. Inside the CPU, one unit recognizes instructions, splits tasks, and assigns them. Other units do the actual calculations, while some pass information and manage resources. Computing is an abstract idea, not just mathematics. Its most basic structures are circuits switching on and off.

## 4. Instructions, parallel computing, and von Neumann architecture

The controller first recognizes instructions. More precisely, it does not "understand" them like a person. Outside forces make its circuits take different paths. For example, a tape has open and closed holes. Where it is closed, the circuit cannot connect, so current takes another route. This is not the same as a switch statement or conditional jump. It is closer to a sensor. Another example is a key entering a lock and lifting parts inside it.

Once an instruction is recognized, commands can go to other computing units. Assembly instructions provide a reference: tell a unit to calculate, or exchange data between memory and registers.

Parallel computing also matters. In the earlier example, the next unit must wait for the division result. This is a strict mathematical order that cannot change. But we can free that unit to do other work first, since division is slow, then return later. Nothing moves globally; the controller always coordinates resources. This saves time and may reduce hardware size. Efficient resource use requires efficient instructions on the tape.

This is where programmers acquire a role. The earliest programmers directly changed circuits, working much like electronics engineers. Later programmers improved the controller's use of resources. This work was still below the level of drivers. A program error could give a wrong result without an error message, or even burn out the circuit.

Today's machine instructions are at a higher level. The instructions discussed earlier are closer to CPU microcode, mostly controlled only by CPU makers. They are still updated and adjusted, but there is limited room. Modern CPUs have some self-learning ability and can identify common patterns. There were major vulnerabilities called Spectre and Meltdown. Those can be a separate topic.

There are actually two instruction systems inside a CPU. Programmers use machine instructions, which can be exposed externally without burning circuits and can report errors and support debugging. Another internal system decodes external instructions and adjusts internal circuits. The CPU can also disable faulty modules itself. Programmers do not directly touch physical reality. The internal structure of modern CPUs can be discussed separately.

A tape is really memory whose contents are physically fixed. Write its contents into memory, and we have entered von Neumann architecture. The controller is also a computing unit with its own registers. The memory controller writes memory data into those registers. The controller then changes the location of the next instruction to read. The memory controller sees this and supplies another instruction. The controller could also request it actively; there is no real difference.

We are not yet discussing any commercial CPU architecture. More precisely, one instruction is a fixed-length group of zeros and ones. Another interesting ability is changing code at runtime instead of using only a fixed tape. This can improve efficiency further. For example, a tape can only specify a fixed memory address for a unit to read. Now that address can be changed directly so it reads another area. This removes a kind of physical hardware related to memory mapping. It may never have existed, but without changing memory at runtime, such hardware would have to appear.

Machines of that time could still be paused and debugged by hand. If needed, a breakpoint could let a person analyze the state and directly change memory bits. Memory data could even be shown directly as lights.

## 5. Storage, networks, and input and output

A hard drive is better described as long-term storage. The earliest form was probably magnetic tape. Physically, magnetic tape consists of many "xxx." Early storage faced data loss and damage, and space was valuable.

A network is not only about connecting computers. More importantly, it tolerates asynchronous operation. A computer normally has many computing units linked by resonance, cycles, or synchronization. A network has no such synchronization requirement. A network cable can be misleading. It actually has eight wires. Apart from power, each side has its own data line, and they do not occupy each other's line. Network hardware manages this, so there are really two lines that do not interfere. A major part of a network card is a cache. It listens to the line, gradually stores data, and lets the CPU read it regularly. Electrical signals remain on both sides even when no information is being sent.

There are reasons networks did not appear earlier: they cost more and have strict timing needs. A network might be better called "two-way radio in a closed circuit." Radio needs transmitters and receivers. This belongs to classical electronics.

Displays have always existed, and memory could sometimes be seen directly. Early systems could also read data from a disk, then write it to a disk or print it. Printers have very simple, mechanical structures.

Even a basic text terminal must handle character input and output, parsing, and storing user intentions. It may even need temporary extra instructions. Just arranging data into an orderly text interface uses many resources. Displays were therefore once hard to accept.

Input and output devices appeared independently of displays. The main early need was to view and change memory data. Once memory was too large to show with lights, parts of it had to be displayed and edited. Early terminals were literally terminals, with separate hardware but almost no modern instructions. They mainly read and wrote data, not only memory but also registers and temporary registers inside hardware. They might even temporarily enable or disable a computing unit.
