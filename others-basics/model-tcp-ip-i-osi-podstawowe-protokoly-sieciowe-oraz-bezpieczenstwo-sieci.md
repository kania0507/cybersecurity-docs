# Model TCP/IP i OSI, podstawowe protokoły sieciowe oraz bezpieczeństwo sieci

### **Model OSI i TCP/IP – jak działają sieci**

W komunikacji sieciowej dane muszą przejść przez różne **warstwy**, które odpowiadają za różne zadania — od fizycznego przesyłu sygnału po działanie aplikacji (np. przeglądarki).\
Istnieją dwa główne modele: **OSI (7 warstw)** i **TCP/IP (4 warstwy)**.

***

#### **Porównanie modeli OSI i TCP/IP**

| **Model OSI (7 warstw)**       | **Model TCP/IP (4 warstwy)**          | **Opis funkcji**                                                                              |
| ------------------------------ | ------------------------------------- | --------------------------------------------------------------------------------------------- |
| 7️⃣ Aplikacji (Application)    | 4️⃣ Aplikacji (Application)           | Komunikacja z użytkownikiem – przeglądarka, e-mail, logowanie (np. HTTP, FTP, SMTP, DNS, SSH) |
| 6️⃣ Prezentacji (Presentation) | 4️⃣ Aplikacji (Application)           | Kodowanie, kompresja, szyfrowanie danych (np. TLS/SSL)                                        |
| 5️⃣ Sesji (Session)            | 4️⃣ Aplikacji (Application)           | Utrzymanie sesji komunikacyjnej (np. logowanie do serwera SSH)                                |
| 4️⃣ Transportowa (Transport)   | 3️⃣ Transportowa (Transport)          | Zapewnia dostarczenie danych – TCP (pewne), UDP (szybkie, bez potwierdzeń)                    |
| 3️⃣ Sieciowa (Network)         | 2️⃣ Internetowa (Internet)            | Trasowanie pakietów w sieci, adresacja IP (np. IP, ICMP)                                      |
| 2️⃣ Łącza danych (Data Link)   | 1️⃣ Dostępu do sieci (Network Access) | Ramki, adresy MAC, błędy transmisji (Ethernet, Wi-Fi)                                         |
| 1️⃣ Fizyczna (Physical)        | 1️⃣ Dostępu do sieci (Network Access) | Przesyłanie bitów przez medium (kabel, fale radiowe)                                          |

**W skrócie:**\
Model **TCP/IP** jest uproszczoną wersją **OSI** – praktyczniejszą i rzeczywiście używaną w Internecie.

***

### **Podstawowe protokoły sieciowe i ich warstwy**

| **Protokół**                             | **Warstwa OSI**         | **Warstwa TCP/IP** | **Zastosowanie**                           | **Bezpieczeństwo**                                                   |
| ---------------------------------------- | ----------------------- | ------------------ | ------------------------------------------ | -------------------------------------------------------------------- |
| **HTTP (HyperText Transfer Protocol)**   | Aplikacji               | Aplikacji          | Przesyłanie stron WWW                      | Brak szyfrowania – dane w jawnym tekście. Stosuj **HTTPS** (TLS).    |
| **HTTPS (HTTP Secure)**                  | Aplikacji + Prezentacji | Aplikacji          | Bezpieczna komunikacja WWW                 | Szyfrowanie TLS – chroni przed podsłuchem i MITM.                    |
| **DNS (Domain Name System)**             | Aplikacji               | Aplikacji          | Zamiana nazw domen na adresy IP            | Zabezpieczenia: **DNSSEC**, **DNS over HTTPS (DoH)**.                |
| **SSH (Secure Shell)**                   | Aplikacji + Sesji       | Aplikacji          | Zdalne logowanie i administracja serwerami | Szyfrowane połączenie i uwierzytelnianie kluczem.                    |
| **FTP (File Transfer Protocol)**         | Aplikacji               | Aplikacji          | Przesyłanie plików                         | Brak szyfrowania – stosuj **FTPS** lub **SFTP (SSH File Transfer)**. |
| **SMTP (Simple Mail Transfer Protocol)** | Aplikacji               | Aplikacji          | Wysyłanie e-maili                          | Stosuj **STARTTLS** lub **SMTPS** (szyfrowanie).                     |

***

### **Bezpieczeństwo sieci – najważniejsze pojęcia**

#### **Podstawowe zagrożenia:**

* **Sniffing (podsłuchiwanie)** – przechwytywanie danych w sieci nieszyfrowanej.
* **Man-in-the-Middle (MITM)** – atakujący w środku połączenia zmienia dane.
* **Phishing / DNS spoofing** – przekierowanie użytkownika na fałszywe strony.
* **DoS / DDoS** – ataki przeciążające serwery.
* **Nieaktualne oprogramowanie** – otwarte luki bezpieczeństwa.

***

#### **Środki ochrony i dobre praktyki:**

| **Mechanizm / Technologia**                               | **Cel / Funkcja**                                |
| --------------------------------------------------------- | ------------------------------------------------ |
| **TLS / SSL**                                             | Szyfrowanie transmisji (HTTPS, SMTPS, FTPS).     |
| **Firewall (zapora sieciowa)**                            | Blokuje nieautoryzowany ruch.                    |
| **VPN (Virtual Private Network)**                         | Szyfrowany tunel do zdalnego dostępu.            |
| **IDS / IPS (systemy detekcji i zapobiegania włamaniom)** | Monitorowanie i blokowanie podejrzanych działań. |
| **Segmentacja sieci / VLAN**                              | Ogranicza rozprzestrzenianie się ataków.         |
| **Silne uwierzytelnianie**                                | Hasła, klucze SSH, MFA.                          |
| **Aktualizacje i łatki**                                  | Usuwają znane podatności.                        |
| **Szyfrowanie danych w spoczynku**                        | Ochrona danych na dyskach i w bazach.            |

***

### **Podsumowanie – w skrócie**

🔹 **Model OSI** – 7 warstw teoretycznych opisujących komunikację w sieci.\
🔹 **Model TCP/IP** – 4 praktyczne warstwy używane w Internecie.\
🔹 **Protokoły (HTTP, DNS, SSH, FTP, SMTP)** – umożliwiają codzienną komunikację sieciową.\
🔹 **Bezpieczeństwo sieci** – opiera się na **szyfrowaniu, kontroli dostępu, firewallach i aktualizacjach**.\
🔹 **Cel:** zapewnić **poufność, integralność i dostępność** danych (tzw. **CIA triada**).
