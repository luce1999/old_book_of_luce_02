## 1. Browsers and page requests

First, let us talk about browsers. A browser is a large project with millions of lines of code. It is very hard to develop. It must support old protocols, while page structures themselves are complex. It also has to handle loading many pages, security such as preventing virtual machine escapes, and rendering.

You can also build your own browser with your own network protocol. Basically, building it on HTTPS is enough.

Suppose we enter a web address. What happens? First there is a DNS lookup, though the computer and browser usually have caches. Then communication uses HTTPS. The HTTPS protocol is very simple, almost plain text. It is basically a GET request: ask for something and receive data. The file header describes the remaining content, data offsets, and so on. HTTPS then gives us an HTML file, meaning Hypertext Markup Language. It also contains JS, a scripting language. At this point it can be rendered. Of course, it can also move to a more modern framework.

## 2. HTTP, DNS, and HTTPS

HTTPS has versions 1.1 and 2. I suggest using 2 by default while supporting 1.1. One benefit of HTTP/2 is multiplexing and header compression. Simply put, this reduces problems such as data waiting in a queue. WebSocket is an upgrade of the HTTPS protocol. `ws` also has some design details you can look into yourself.

DNS has several request methods, but an intermediary may poison the results. DNS is not encrypted by default. Even without an intermediary doing this, the DNS provider may do it. Sometimes a DNS lookup is still necessary because IP addresses can change or a website has not been visited before. Make lookups when needed, and use caching and comparisons properly.

Most websites now use HTTPS, meaning encrypted connections. Even if an intermediary cannot see the content, the website itself may still sell user information.

## 3. Keys and encryption

A TLS handshake uses certain mathematical rules. Simply put, one value can be calculated into another value B. The algorithm can be ECC, or elliptic curve encryption, or another kind such as RSA. It also needs a private key and a public key. One side can encrypt with the public key, and the other can decrypt with the private key. That is just its mathematical property; I do not know why either. But quantum computers can break it, reducing exponential cracking time to polynomial time. It seems to use some kind of vibration in higher dimensions.

That was the most traditional RSA communication, with only one public key and one private key. The public key is normally made public. Users use it to send messages to the server. Even if the messages are intercepted, only the holder of the private key can read them. The problem is that poor website management can leak the private key. Transmitted content may have been recorded earlier and can then be decrypted.

The solution is forward encryption. In simple terms, create a temporary public and private key pair, use it, then discard it. After establishing a channel, generate a new key pair and use that.

Another kind is AES. It is symmetric encryption: encryption and decryption use the same key, and performance is high. Usually, an asymmetric handshake comes first. The two sides then agree on an AES key and communicate using AES. The underlying encryption generally uses AES or xxx. It may then add zeros at the end, exchange some data, rotate keys, and so on. The details depend on the rules.

## 4. Certificates and connections

Next are certificates. Certificates also use asymmetric encryption. The user sends a random number. The server calculates with its private key and sends the result back. The user checks it with the public key. This confirms that the server can use the private key, so it is the server. There is therefore a firm guarantee that does not depend on DNS or IP.

However, certificates are generally tied to IP addresses. I suggest not tying them to IPs and using direct queries instead. Also, do not use the system CA, because it could be attacked. I suggest hard-coding the server's public key in the client, without storing it on disk or depending on anything external.

I will also mention QUIC, or HTTPS 3. It uses UDP and is better for video. It can use several routes, and order does not matter. It can also find a suitable route when the network changes, such as when a phone's mobile connection switches to another route.

## 5. How pages run and connect

A web page is really a program running in a virtual machine, using WASM. Its overhead is low because modern CPUs provide a hypervisor that can execute CPU instructions with almost no loss. It can also create other connections of its own. So opening a page actually creates many connections, including WebRTC. This may leak your IP, so do not click unknown emails. Email systems are very outdated; we can discuss that another time. You can actually run your own email website, but other major services may not accept it because of industry reputation issues.

IP routing also has a NAT problem. The network provider needs to map addresses because sometimes there are not enough IPs. There can be several layers of NAT, starting with the router.

A fixed IPv4 address has 65536 ports, allowing different services on different ports. 65536 is 256 × 256. Providers usually block packets other than UDP and TCP. They also block some ports for ordinary users, such as 80 and 443.

## 6. TCP, UDP, and TLS

TCP and UDP are abstractions provided by the operating system. What finally goes out is raw network packets. The operating system packages TCP and UDP on top of IP for programs to use. A program first asks to create a TCP connection, then calls the Windows API so the operating system can push data into it. The operating system processes the data based on its length and other details, then sends it. It also handles data errors and ordering errors internally.

One main problem with TLS 1.2 is that it has too many protocols and too much variety. TLS 1.3 has a way to prevent downgrades to TLS 1.2. For example, both sides agree to use TLS 1.3, but an intermediary changes the messages to make each side appear to support only TLS 1.2. At the end, hashes of the conversation records are checked. A mismatch shows that the messages were changed, and the connection ends.

At first, communication mainly relied on dedicated lines and simple encryption. Later came encryption that could be widely used on the internet. Many encryption methods before TLS 1.2 had vulnerabilities that made them fail completely. So the structure must be correct both mathematically and in the program. You can look into it if you are interested.
