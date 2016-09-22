#Tuesday, September 6th
* It feels like I've been gone for a long time...
* A little exercise:
  - When you hear the term information security, list some topics, issues, or things that come to mind.
  - List some information security events that have occurred this calendar year.
* Terminology: Is it Computer Security?  Is it Information Security (infosec)?  Is it Cyber Security?
* The schtick is very different in this course, and this may be arguably the most "different" course you will take in the CS curriculum
* By definition, what is security?
* So how far have we come? (or lack thereof)
* One outcome of this course: question everything
* What's my ultimate goal for you in this course?  We'll revisit this on the last day of class.
* Virtual Machine

#Thursday, September 8th: Social Engineering
* PSA
* Social Engineering
* But, if most Security problems are human-based, then why do we need to focus on exploits, vulnerabilities, the tech stuff?
* Watch: Tacoma Narrows Bridge Fail
* What's the point?

#Tuesday, September 13th: Networking 101
* Last class: social engineering, the achilles heal known as software.  Two very hard problems.
* Read "Trusting Trust".  For most of this course, we will talk about the hard problem of software security.
* The "Trinity of Trouble" by Gary McGraw
	- Complexity
	- Extensibility
	- Connectivity
* Why study networking?
	- The "Connectivity" issue
	- Where the "cool stuff" happens
	- The cyber attribution problem => https://twitter.com/thegrugq/status/706545282645757952
* Recall the telephone conversation analogy for basic networking stuff
* Take it a step further: the OSI model and the seven layers
* Analogy for the OSI model: the US Postal Service => http://bpastudio.csudh.edu/fac/lpress/471/hout/netech/postofficelayers.htm
* Get comfortable reading Request For Proposals (RFPs):
	- Internet Protocol (IP): RFC 791 => http://www.ietf.org/rfc/rfc791.txt
	- Transfer Control Protocol (TCP): RFC 793 => http://www.ietf.org/rfc/rfc793.txt
* A packet: contains implementations of all the protocol layers; encapsulation model
* A PCAP: a file of packet captures from a network
* The Wall of Sheep
* tcpdump, Wireshark, ettercap
* The next lab

#Thursday, September 15th: Sniffing
* So you may be curious: how did we capture all those packets?
* tcpdump, ifconfig
* Two types of networks:
  1. Unswitched - packets flow through all devices on network but you look at only the packets addressed to you......
    - Welp... http://superuser.com/questions/191191/where-can-i-find-an-unswitched-ethernet-hub
  2. Switched - packets flow through specific devices on network
* Promiscuous mode
* Preventing sniffing:
  1. Use encryption and encrypted network protocols
  2. VPN
  3. Use switched network......?
* LAN Tap: http://hakshop.myshopify.com/products/throwing-star-lan-tap-pro
* Address Resolution Protocol
  * IP address to MAC address on a network
  * Recall OSI model and packets
  * `arp -a`
  * ARP cache on machine for 20 minutes
  * No authentication
* ARP spoofing or ARP poisoning

#Tuesday, September 20th: Scanning
* Last class: sniffing unswitched and switched networks
* Is sniffing still relevant today?
* Preventing sniffing on switched network:
  * anti-arpspoof
  * ArpON
  * Antidote
  * Arpwatch
* About that problem on the PCAPs lab
  * A goal of this class: recognition and mindset
  * Base64: binary-to-text encoding scheme.  That is: binary data to ASCII
  * http://stackoverflow.com/questions/6916805/why-does-a-base64-encoded-string-have-an-sign-at-the-end
  * Why? Dangers in printing payload: https://unix.stackexchange.com/questions/73713/how-safe-is-it-to-cat-an-arbitrary-file
  * Why? Basic authentication on web. Example: https://github.com/LiamRandall/BsidesDC-Training/blob/master/http-auth/http-basic-auth-multiple-failures.pcap
* Scanning
  * Why? Network reconnaissance.  Warfare 101
  * What devices and computers are up?
  * What ports are open on a computer?
  * What services are running
  * Determine possible vulnerabilities
* Is scanning still relevant today?
* Basic method: ping sweep
* Problems with ping?
* Netcat
* Nmap

#Tuesday, September 22nd: Scanning, Part II
* Recall scanning:
  - Think poking holes, "ask questions"
* Poking holes => finding interesting and unwanted stuff on networks
  - Shodan: https://www.shodan.io/
* What could possibly go wrong?
* Want to be stealthy!
* RFC 793: if ports are closed and you send "junk" to it, RST packet will be sent! (page 65)
  * FIN scan: `sudo nmap -sF ...`
  * NULL scan: `sudo nmap -sN ...`
  * XMAS scan: `sudo nmap -sX ...' # FIN, PSH, URG flags in packet]
* Decoy:
  * `sudo nmap -D...`
  * spoofed connections
  * Must use real + alive IP address, else SYN flood
* SYN flood
  * The idea: exhaust states in the TCP/IP stack
  * Recall TCP/IP handshaking
  * Attacker sends SYN packets with a spoofed source address, the victim, (that goes nowhere)
  * Victim sends SYN/ACK packet but attacker stays slient
  * Half-open connections must time out which may take a while
  * Alas, good SYN packets will not be able to go through
* Defending against scanners
  * No certain way
  * Firewalls?
  * Close services
  * Packet filtering
* Defending against SYN flood
  * Increase queue
  * Filtering
  * SYN cookies
  * Reduce timer for SYN packets

#Tuesday, September 27th: The Oldie But Goodie Networking Attacks
* Amplication attack, Denial of Service
  - Smurf
* https://blog.cloudflare.com/deep-inside-a-dns-amplification-ddos-attack/
* Someone I know: Brian Krebs http://krebsonsecurity.com/2016/09/krebsonsecurity-hit-with-record-ddos/