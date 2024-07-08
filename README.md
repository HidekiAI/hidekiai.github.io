# hidekiai.github.io
Ittsah miiiii!  HidekiAI!

👋 Hi, I’m @HidekiAI (Hideki A. Ikeda), I've "profressionally" been programming since April 1989.

My first professional job was mainly in Assembly lanaguage - 6502/65C816, Z80, Motorolla 68000, as well as C.

Other languages I can safely get by (because I've coded professionally) are C++11, C#, and F#.

My professional experiences have been mainly been reflected by video game industries, but as hobbies and self educations, I do try to keep up with other intersts such as machine-learning and microservices.

🌱 I’m currently (and probably never stop) learning C++17 (for stability in libraries) and Rust (for functional aspect with C++ performance) for several years, and IMHO Rust is my all-time favorite.

👀 The projects you'd find here: I’m interested in writing/working on projects that are somewhat useless (useful TO ME, but not too useful to you) but FUN TO ME... They are mainly in the languages I fancy at the moment, but at times the language chosen are mainly because of the supported libraries.

💞️ I’m looking to collaborate on any open source libraries that are network-oriented, but am also interested in video game related libraries and projects.

📫 I guess you can reach me on LinkedIn username HidekiAI


## Interview questions I'd like to ask others:

- Write a parser (in language of your choice, including BASH) to read in string that is either a hostname or an IP address, and the address can optionally have a ":" that indicates port.  Example: "127.0.0.1:22", "localhost:443", "myhostname", "myhostname.localdomain.tld", "::1".  Ideally, this is great if it is a take-home question, especially because it can become an unfair question when IPv6 is involved or a host is multi-homed 
  - hint: IP address can be either IPv4 or IPv6
  - hint: IPv6 and port combination will make it complicated for programmers who may be seeking for last encounter of ":" to mean port because address such as "8080::80:80" will become ambigous:
    ```bash
    $ ipv6calc --addr_to_uncompressed 8080:80::80:80
    8080:80:0:0:0:0:80:80
    ```
  - hint: the smart people on the Internet has defined the format (for URI) to be `[8080:80::80]:80` to be the format to avoid ambiguities
  - hint: "eye-balling" towards IPv4 over IPv6 when DNS returns both
  - hint: how to bias on multi-homed hosts via looking up routing table (i.e. `ip route` command)
- What is the theoretical number of connections a single server can have?
  - hint: port is 16-bit, hence ports can range from 0..65535 (0xFFff)
  - hint: sockets have in-buffer and out-buffer (2 memory pools) at kernel level, but when you create a socket, you would usually create your own (i.e. circular queue) buffer for asynchronous read and asynchronous writes
  - hint: Wikipedia says it's about 10K but does not say whether that its on 64-bit Linux or Windows, or 32-bits Linux and/or Windows servers.  It does not mention whether that is due to limiations on RAM at kernel level (i.e. Layer 2) or application (i.e. Layer 4) level.
  - One of the neatest examples I can give is tarpitting to counter ping-of-death because it allocates 0-bytes at kernel level, as well as healthy debates on whether tarpits are really entrapment...
- SPAM Service Part1: Write a very simple SPAM filter (in the language of your choice, including BASH) that you can add rules in a "rules.lst" file, where the rules are basically `command:value`.  The supported commands are initally `email:<email addresses>` and `subject:<keywords` where both email addresses and keywords accepts wildcard `*` (i.e. `*.bad-domain.net`, `send * dollars to`, etc).  The response is very simple, it will return a value between 0.0 and 1.0 (`float32`) in which 1.0 means 100% match confidence/probability that it's a SPAM, where 0.0 means no confidence at all (not a SPAM).
- SPAM Service Part2: Discuss system designs with an assumption that this SPAM filter service will be a micro-service.
  - How is this micro-service receiving its input?  Pub-Sub? RPC? REST?
    - What happens if the micro-service crashes while it's deciding its probability?
    - What happens if the requested mail-server crashed?  acknowledge/confirmation receipt?
    - Should the requesting mail-server time-out?  Hint: most common mail-server that supports for example SpamAssasin, approaches are to forward the e-mail into the queue and completely remove it from its own mail queue.  The forwarded service (SpamAssasin) receives it as a persisted data and once it evaluates it, it will then get added back to the mail-server's queue with the subject revised to  `[SPAM]: <original subject>` (if it was a SPAM), and sent/received timestamp preserved.
    - How is this micro-service responding its output to the requested mail-service?
  - What if there are more than one instance of the service, how can it share the "rules" list?  Does it make sense to be a file? DB? NoSQL?
