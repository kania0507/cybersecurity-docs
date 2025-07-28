# CompTia Sec+ treats, atacks and vulnerabilities

**Types of Malware:**

o Virus: An unsolicited and unwanted malicious program.\
o Worm: A self-contained infec6on that can spread itself through networks, E-mails, and messages.\
o Crypto-Malware: A malicious program that encrypts files on the computer to extort money from the user.\
o Ransomware: Denies access to a computer system or data un6l a ransom is paid. Can be spread through a\
phishing E-mail or an unknowingly infected website.\
o Adware: A program that produces ads and pop-ups using a browser. May replace the original browser\
and/or produce fake ads to “remove” the adware, which only downloads more malware.\
o Spyware: SoGware that installs itself to spy on the infected machine and sends stolen informa6on back to\
the host machine.\
o Keylogger: A malicious program that records keystrokes from the infected machine.\
o Logic Bomb: A malicious program that lies dormant un6l a specific date or event occurs.\
o Bots: AI that performs specific ac6ons as a part of a larger en6ty known as a botnet.\
o Trojan: A form of malware that pretends to be a harmless applica6on.\
o Remote Access Trojan (RAT): A remotely operated Trojan.\
o Rootkit: A backdoor program that allows full remote access to a system.\
o Backdoor: Allows for full access to a system remotely.



**Types of Attacks:**

o **Social Engineering**\
Phishing: Sending false E-mails pretending to be legitimate to steal informa6on from the user.\
§ Spear Phishing: Attacks that target specific users.\
§ Whaling: A targeted aLack on a powerful or wealthy individual.\
§ Vishing: An aLack through a phone or voice communica6on.\
§ Smishing: An aLack through SMS.\
§ TailgaHng/Piggybacking: Closely following authorized individuals to get access to secure areas.\
§ ImpersonaHon: Taking on the iden6ty of an individual to gain access to a system.\
§ Dumpster Diving: Going through trash to find thrown-away valuable informa6on or possessions.\
§ Shoulder Surfing: Watching as a person enters informa6on.\
§ Hoax: Deceiving the user into compromising security by falsely making them believe they are at risk.\
§ Watering Hole: Targets a group by infec6ng a website that is commonly visited by the members.\
&#x20;• Principles of Social Engineering/ Reasons for EffecHveness\
&#x20;    o Authority: Behaving as an individual with authority.\
&#x20;    o InHmidaHon: Frightening or threatening the vic6m.\
&#x20;    o Consensus: Influencing others based on what peers do or are said to do.\
&#x20;    o Scarcity: Limi6ng resources or 6me to act.\
&#x20;    o Familiarity: Behaving like a familiar person to the vic6m.\
&#x20;    o Trust: Gaining the vic6m’s confidence or being their “friend.”\
&#x20;    o Urgency: Limi6ng 6me to act. Rushing the vic6m

o **Application and Service Attacks**&#x20;

§ Denial of Service (DoS): Flooding a target machine to prevent the use of its resources.\
§ Distributed Denial of Service (DDoS): Mul6ple different sources aLack one vic6m.\
§ Man-in-the-Middle: The aLacker alters the communica6on between two par6es who believe they\
are directly communica6ng.\
§ Buffer Overflow: A program writes more data than can be held in a fixed block of memory.\
§ InjecHon: Inser6ng code into a vulnerable computer program and changing the course of execu6on.\
§ Cross-Site ScripHng (XXS): Found in web applica6ons. Allows for an aLacker to inject client-side\
scripts into web pages.\
§ Cross-Site Request Forgery (XSRF): Unauthorized commands are sent from a user that is trusted by\
the website. Allows the aLacker to steal cookies and harvest passwords.\
§ Privilege EscalaHon: Exploits a vulnerability that allows an aLacker to gain access to resources that\
they normally would be restricted from accessing.\
§ ARP Poisoning: The act of falsifying the IP-to-MAC address resolu6on system employed by TCP/IP.\
§ AmplificaHon: The amount of traffic sent by the aLacker is originally small but then is repeatability\
mul6plied in an aLempt to cause the vic6m machine to fail or malfunc6on.\
§ DNS Poisoning: Exploits vulnerabili6es in the Domain Name System (DNS) to divert Internet traffic\
away from legi6mate servers and towards fake ones.\
§ Domain Hijacking: Changing the registra6on of a domain name without the vic6m’s permission.\
§ Man-in-the-Browser: A proxy Trojan horse that infects web browsers and captures session data.\
§ Zero Day: Exploits for which there is no known defense.\
§ Replay: Valid data transmission is rebroadcasted, repeated, or delayed.\
§ Pass-the-Hash: An authen6ca6on aLack that captures and uses password hashes. The aLacker\
aLempts to log on as the user with the stolen hash. This bypasses the need to decrypt passwords.\
§ MAC Spoofing: The aLacker falsifies the MAC address of a device.\
§ IP Spoofing: An intruder uses another site's IP address to masquerade as a legi6mate site.

**Hijacking Attacks**\
§ Clickjacking: Deceives the user into clicking on a malicious link by adding the link to a transparent\
layer over what appears to be a legi6mate web page.\
§ Session Hijacking: An aLacker impersonates the user by using their legi6mate session token.\
§ URL Hijacking/ Typo-squa\[ng: Redirects the user to a false website based on a misspelled URL.\
o Driver ManipulaHon\
§ Shimming: Injec6ng alternate or compensa6on code into a system in order to alter its opera6ons\
without changing the original or exis6ng code.\
§ Refactoring: Rewrites the internal processing of code without changing its behavior.\
o Wireless ATacks\
§ Replay: This is a passive aLack where the aLacker captures wireless data, records it, and then sends\
it on to the original recipient without them being aware of the aLacker's presence.\
§ Evil Twin: An Access Point (AP) that has the same Service Set Iden?fier (SSID) as a legi6mate Access\
Point. Once a user connects to it, all wireless traffic goes through it instead of the real AP.\
§ Rogue Access Point: An unauthorized Wireless Access Point (WAP) or router that is designed to\
bypass network security configura6ons but opens the network and its users to aLacks.\
§ Jamming: Disabling a wireless frequency with noise to block the wireless traffic.\
§ Wi-Fi Protected Setup (WPS): Allows users to easily configure a wireless network, some6mes by\
using only a PIN. The PIN can easily be found through a brute force aDack.\
§ Bluejacking: Sending unauthorized messages to a Bluetooth device.\
§ Bluesnarfing: Gaining unauthorized access to or stealing informa6on from a Bluetooth device.\
§ Radio Frequency IdenHfier (RFID): Communicates with a tag placed in or aLached to an object using\
radio signals. Can be jammed with noise interference, the blocking of radio signals, or\
removing/disabling the tags themselves.\
§ Near Field CommunicaHon (NFC): A wireless technology that allows for smartphones and other\
devices to establish communica6on over a short distance.\
§ DisassociaHon: Removes clients from a wireless network. A form of Denial of Service (DoS).\
\
**Cryptographic Attacks:**\
§ **Brute Force**: A password-cracking program that systemattically guesses every possible combination\
of characters until the correct password is found.\
§ **Dictionary**: Creates encrypted versions of common dictionary words and then compares them\
against those in a stolen password file. Guessing using a list of possible passwords.\
§ **Rainbow Tables**: Large pre-generated data sets of encrypted passwords used in password aLacks.\
§ **Birthday**: Used to find collisions in hashes and allows the attacker to create the same hash as the\
user. Exploits the fact that if the same mathematical function is performed on two values and the\
result is the same, then the original values must be the same.\
§ **Collision**: When two different inputs produce the same hash value.\
§ **Replay**: The attacker captures network packets and then retransmits them back onto the network to\
gain unauthorized access.\
§ **Weak Implementations**: The main cause of failure in modern cryptographic systems are due to poor\
or weak implementations as opposed to a failure caused by the algorithm itself.\
§ **Downgrade**: Forces a system to lessen its security, allowing the aLacker to exploit the lesser\
security control. It is most often caused by weak implementations or deprecated cipher suites.



_(C) By Krystal Ballew_
