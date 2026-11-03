## 1. Desktop and workspaces

Here I will bring together the design ideas for an operating system. For now, I call it Brutus.

For the user experience, there are two workspaces by default, though the number can change. The screen is split into two parts. This is operating-system-level help, mainly to improve productivity. For example, you can view a website on one side and other content on the other. Windows desktops can already do this, but it is less native and more troublesome. Existing web systems will be kept and supported. Our own web system will fit split views on one screen more naturally, and will support several displays.

Other window settings are allowed, such as keeping a window on top. In Windows, a program usually needs to call an API itself for this. Here, all windows should be able to do it.

Workspaces can also represent work modes. The operating system starts in a general mode. Users can set up one or more work modes. Inside a mode, only a limited area can be accessed, and its environment is isolated from other areas. Programs can only be installed in that area. Some of this was previously done by "xxx," but now the operating system should provide the isolation. Confusing environment management is still a problem, so this will suit developers well. Settings and window positions can be saved at shutdown, and startup items can be set. Many of these ideas come from problems I have had while using computers.

Simply put, it is like opening a virtual machine, but it is not a hypervisor, so that is not a problem. The kernel guarantees isolation. I once clicked the wrong folder and performed an action there by mistake. That could be very dangerous. Colors and symbols can distinguish areas. Custom skins can improve ergonomics and avoid disastrous results. Windows can also stick together and be dragged as a group.

## 2. Windows, programs, and interaction

Built-in windows such as the file manager and settings all use browser rendering. I think this is fairly modern and reduces frontend errors and vulnerabilities. Of course, we will not directly use existing systems such as xxx. We will have our own lighter web system. This part will not try to support existing systems. The aim is to be lighter and more varied.

Windows allow right-click actions. Normally a window must be clicked before you can operate it, though this can be customized. A focused window is highlighted to prevent wrong clicks. Pages will also have slide-to-unlock controls to prevent accidental actions.

Programs must be installed before use. They cannot operate directly in their own root directory. Programs are completely separated from disks. Each run gets a temporary environment, and several isolated instances can run at once.

A more important design goal is that all computer functions must be usable with only a keyboard or only a mouse. The operating system must guarantee this and ensure programs support it too.

We also want to unify the GUI and console. What the GUI shows must be exactly the same as the console content. Rather than a GUI, it is a more modern console. It will look more like a chat page with several buttons and input fields. Program output is categorized, and users can filter and search it manually. Help documents will also be available.

The operating system also supports multiple seats. One computer can have two displays and two sets of keyboards and mice, isolated from each other. For example, one person can start with administrator rights, while the other cannot install software but can play games and browse websites. There is normally no performance loss, although two people gaming at once may be limited by GPU performance. Gaming while another person watches video is usually fine. When a web page is covered, the operating system can stop video rendering and save resources automatically. Two displays may create a heavier load, so a good background and push system is needed. Programs should run with low resource use while still receiving notifications.

Better connections with other devices, such as Android devices, are also needed. This may require installing software on an Android phone.

## 3. Program loading and the file system

The way programs load disk data will change. The operating system transfers it in 4 KB units and loads each as a page, rather than traditional xxx. This is closer to loading a DLL. Programs and disks are completely isolated. The operating system no longer exposes a complete file list to programs. Each program has its own working environment. It can submit content to the operating system in a write-only way, instead of first creating a file and writing it byte by byte.

Traditional Linux string-based paths will be dropped completely. Two `uint64` values will represent a file. Its name is only an attribute. Reading and writing mainly use 4 KB units. The operating system then automatically compresses and backs up storage. It will also offer a xxx method related to virtual addresses and a way to deploy program description files.

Remote and local desktops will be exactly the same. The difference between remote and local use will be ignored more naturally. Even when logging in locally with a display and keyboard, what you see and how you work will be exactly the same as access over a network. The operating system can still tell them apart and allow configuration.

Desktop access uses a special protocol, temporarily called xxx. It has three main parts: page declarations, event delivery, and live image transmission. Live images are like 3D game rendering. Page declarations describe windows, titles, and buttons. Events describe actions such as which button was clicked. Mouse movement is normally not captured.

## 4. Office deployment and servers

The design is not just for personal PCs. It will also seriously consider centralized office deployment and server use. For example, a group of ordinary office computers can connect to one powerful server. Those computers can run xxx or our xxx and connect through a remote desktop. Company computers can also have monitoring software.

After a computer is installed for an ordinary employee, a key is provided. Administrators can log in from outside, while employees use a restricted mode. Employee computers can have very low specifications. They only need to show a picture and support a keyboard and mouse. The server supplies the main computing power, and a low-bandwidth method such as xxx sends the result to the employee computer.

This concentrates powerful chips in the server and keeps data there too. Employees do not need to configure environments themselves and can continue working after leaving the office. Other external devices can also connect. For example, an office can have a USB reader. Instead of plugging a drive into a computer, you plug it into that device. It submits data to the server for analysis, then provides business-level results to the employee. Employees do not need to worry about computer details. They can also see current and long-term server performance use.

Server processing will be fast, especially for large amounts of data. External devices can also share data through accounts. More importantly, all data stays on one server or a server cluster. It does not need to move back and forth. Employees only need access rights to read it. The company must set up those rights beforehand. Operating system APIs will be simplified and designed carefully. Related miscellaneous actions will become one API, with parameters choosing the action, reducing the API count.

## 5. Applications, permissions, and security

There will also be a special kind of program, called BCVM. It has further limits and only keeps business logic. Other abilities must use plugins provided by the VM. It resembles Android programs, with bytecode and an interpreter, but its components are also custom-made. Components can be updated without updating the program. These programs are safe and nearly plain text to the operating system, so potential problems can be identified. Performance is a little lower. The operating system could also compile them locally into native binary code.

This suits small applications, which users can develop or download. Because the content can be inspected, it is safer and can improve the experience quickly. Application-level CA certificate management is also needed. Ordinary programs can call it or choose not to use it. Cryptography must consider post-quantum methods. My idea is to open another channel after a TLS 1.3 handshake. Even if the post-quantum method later proves flawed, TLS can still provide protection.

The operating system will offer custom channels for sound, networks, and so on. Complex settings will not need a virtual sound card. Different audio outputs and sounds can also be supported. Like multiple seats, this connects and isolates devices and users at the hardware level.

The application store allows installation packages to be downloaded. It checks company qualifications and code, and may require source code to some extent. Programs that break the rules can be refused entry. Advertising and information collection are strictly forbidden.

The system will not support existing ecosystems such as Windows, but it will provide a development SDK. Development can use C++ directly, and perhaps even Windows APIs, automatically translated by the toolkit. The whole ecosystem will be developed by us. There will also be engineering SDKs for functions such as saving and opening files and basic 3D rendering, suitable for industrial software. The SDK gives a basic framework that developers can change and extend.

The file system has isolation to stop programs from mistakenly deleting their own files. Files can also be shared with user permission. A flexible file system layer makes more features possible.

Networking will support IPv4, IPv6, TCP, UDP, and so on. Other connection methods will also be offered, such as redirection provided by server applications and encrypted transport channels. We will stop using localhost methods that occupy ports and risk leaks. With proper setup and a relay server, access can even cross machines. Operating-system-level routing lets different websites use separate routes and remain isolated. This suits online commerce and other work needing strong IP protection. In simple terms, there is a built-in software router, with more complex settings such as two network interfaces on one computer. Few operating systems give this level of help. By default, programs cannot reach the outside network. Users must actively enable or request it.

## 6. Console, localization, and permission management

The console mainly needs to solve rollback after failure. It should roll back without loss as much as possible and keep no hidden context. It is closer to an automation protocol than a traditional terminal. Application-level translation software is also needed. It must work locally without depending on large outside companies and fit well with the UI and other features.

The system natively supports UTF, with a built-in input method. I strongly dislike external input methods because I think they create serious privacy problems. The system will provide its own configuration, such as common words. This is actually enough for use.

At present, there is already xxx and applications. Startup is fairly fixed, with little room for change. Next is compatibility with the Linux hardware ecosystem, or translation to achieve it. I am not very satisfied overall, but I now have experience from trying it and plan to try again.

Application management will be very strict. Permissions are assigned by program properties, and network communication is often forbidden. Communication apps may need an open network channel. BCVM is one possible approach: give the program two threads, one handling network transport through the company's API. Even if the other reads sensitive content, it cannot send that content out.

For example, a beauty camera app can upload photos and also has camera access. These two parts can be separated, and users must explicitly choose a specific photo for upload. There may still be watermark problems, so it is not simple. If necessary, we will develop this part ourselves too. I now completely distrust internet companies. I think I have given them enough chances, but have not seen products get better.

The permission system will offer better APIs for cooperation between processes, such as shared pages, and better messaging. Permission requests will not take over the screen. They will appear in settings, which users must actively open and click. This avoids interruption. Permission can be withdrawn after it is given, and direct grants of administrator rights are not allowed.

Programs must not gain administrator rights and then install kernel components. Windows currently has this problem. Once users give administrator rights, programs may install kernel components. Even with a correct signature, the operating system still asks the user to agree. Kernel components should directly require source code submission and be downloaded and installed from the app store, rather than ordinary installers. Third-party mirrors may be allowed, but hashes must be checked to avoid supply chain contamination.

For websites, I suggest tying certificates to domain names. For example, if a higher-level certificate signs a certificate, its domain must be under the higher-level domain.

## 7. Device sharing, automation, and rendering

Old computers can become devices such as a NAS. After installing the operating system, they can provide storage, CPU computing, GPU computing, and memory without a keyboard or display, with support from the operating system. Access needs a key. Third-party programs can also offer those resources to other sites. The main work computer can set up automatic backups to a connected device, or send some logs to that computer with automatic routing.

We will drop traditional file manager settings and provide file-manager-level APIs instead. Users can use Lua 5.1 to change and adjust things themselves, or ask AI to help. Advanced customization through code is allowed at many levels, without side effects such as network transfers or disk writes.

A good clipboard is also needed, with caching and encrypted storage. All programs are forbidden from reading it directly. Only the operating system can actively provide clipboard content through push messages. Successful copying should produce a notification. Content that must not go to disk must never be written there. Mechanical disks do not enable temporary memory caching by default. USB drives must not load automatically, and Bad USB needs protection.

When a keyboard or mouse is plugged in, it must pass movement and key tests to check for abnormal devices. For example, the display asks for the mouse to move to an area and click. An abnormal device that cannot see the display cannot pass. Basic software such as a notepad, calculator, and clock will be provided. Related APIs can be configured and used by users, and can also be intercepted.

One Windows problem is that its GUI strongly works against automation and greatly reduces efficiency. For agents, we can provide ordinary access rights. Users can keep using the computer while agents work in isolated environments. No virtual machine is needed and there is no performance loss.

For interoperability, I strongly dislike making existing apps adapt to several terminals. This is troublesome. The web itself was designed for interoperability. Many parts of our design follow web transmission ideas. They use little bandwidth, keep APIs consistent, perform better, and reduce errors, including app errors that appear only under special conditions.

Finally, page rendering will change. Instead of programs rendering directly, they submit a table to the operating system, which renders everything centrally. This greatly reduces rendering costs and removes the need for a graphics compositor. It is especially useful for weaker devices such as phones. The original direct-rendering method will still be available.
