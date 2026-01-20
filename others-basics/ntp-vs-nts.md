# NTP vs NTS

#### **NTP (Network Time Protocol)**

* **Purpose:**\
  Synchronizes clocks of systems over a network.
* **Port:**\
  Uses **UDP port 123**.
* **Security:**
  * Originally **not secure**—no built-in encryption or authentication.
  * Vulnerable to:
    * Spoofing
    * Man-in-the-middle attacks
    * Reflection/amplification in DDoS
* **Typical Use:**\
  Still widely used for time sync, especially in environments where time accuracy is important but security is not a major concern (e.g., local trusted networks).

***

#### **NTS (Network Time Security)**

* **Purpose:**\
  Adds **security to NTP** through cryptographic protection.
* **How it works:**
  * Uses **TLS** to securely negotiate keys.
  * Protects **NTP packets** from tampering, spoofing, and replay attacks.
* **Security Features:**
  * **Authentication** of time servers
  * **Integrity** of time data
  * **Confidentiality** (to some extent)
* **Standards-based:**\
  Defined in RFC 8915 (published in 2020).
* **Use Case:**\
  Ideal in environments needing **secure and trusted time synchronization**, e.g.:
  * Financial services
  * Government networks
  * Encrypted logging systems

***

#### &#x20;Summary Table

| Feature                 | NTP                   | NTS (NTP + Security)            |
| ----------------------- | --------------------- | ------------------------------- |
| **Protocol**            | Network Time Protocol | Network Time Security extension |
| **Port**                | UDP 123               | TLS (typically port 4460)       |
| **Security**            | None (in basic NTP)   | Secure (auth, integrity)        |
| **Standard**            | RFC 5905              | RFC 8915                        |
| **Vulnerable to MITM?** | Yes                   | No (protected via TLS)          |
| **Use Case**            | General networks      | High-security environments      |

***

> _“Which protocol adds cryptographic security to time synchronization over the network?”_

Correct answer: **NTS**
