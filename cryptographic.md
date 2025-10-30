# Cryptographic

Match cryptographic algorithms to with their most appropriate application:

| Nr    | Zastosowanie                                                                                  | Odpowiedni mechanizm                | Uzasadnienie                                                                                                                         |
| ----- | --------------------------------------------------------------------------------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **1** | **Digital Signatures (podpisy cyfrowe)**                                                      | **RSA / ECC**                       | Używają pary kluczy (publiczny/prywatny) do tworzenia i weryfikacji podpisu cyfrowego. ECC jest nowszą, lżejszą alternatywą dla RSA. |
| **2** | **Encrypting data on mobile devices (szyfrowanie danych na urządzeniach mobilnych)**          | **ECC (lub RSA do wymiany kluczy)** | ECC zapewnia silne szyfrowanie przy małym obciążeniu obliczeniowym — idealne dla urządzeń mobilnych o ograniczonej mocy.             |
| **3** | **Ensuring the integrity of data in transit (zapewnienie integralności danych w transmisji)** | **HMAC**                            | Wykorzystuje wspólny sekret i funkcję hashującą (np. SHA-256), aby wykrywać modyfikacje danych w trakcie przesyłania.                |
| **4** | **Generating secure hash values for passwords (tworzenie bezpiecznych skrótów haseł)**        | **SHA-256**                         | Funkcja skrótu, która tworzy nieodwracalny hash hasła; używana do bezpiecznego przechowywania haseł (często z solą).                 |

***

📘 **Podsumowanie w skrócie:**

| Algorytm      | Główne zastosowanie                    |
| ------------- | -------------------------------------- |
| **RSA / ECC** | Podpisy cyfrowe, szyfrowanie           |
| **HMAC**      | Integralność i uwierzytelnienie danych |
| **SHA-256**   | Hashowanie (np. haseł, plików, danych) |
|               |                                        |
|               |                                        |



Match the network device or application to the correct cryptographic protocol.

| Nr    | Zastosowanie / Urządzenie              | Odpowiedni protokół kryptograficzny    | Uzasadnienie                                                                                                         |
| ----- | -------------------------------------- | -------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **1** | **Web Server**                         | **TLS (Transport Layer Security)**     | Zapewnia szyfrowanie i uwierzytelnianie komunikacji między przeglądarką a serwerem WWW (HTTPS).                      |
| **2** | **Remote Server Access**               | **SSH (Secure Shell)**                 | Umożliwia bezpieczny zdalny dostęp do serwera (np. przez terminal) z szyfrowaniem sesji i uwierzytelnieniem kluczem. |
| **3** | **Email Encryption**                   | **PGP (Pretty Good Privacy)**          | Służy do szyfrowania i podpisywania wiadomości e-mail w celu zapewnienia poufności i autentyczności.                 |
| **4** | **File Encryption on a Local Machine** | **AES (Advanced Encryption Standard)** | Symetryczny algorytm szyfrowania używany do ochrony plików lokalnych przed nieautoryzowanym dostępem.                |

***

📘 **Dodatkowe uwagi:**

| Protokół | Typ kryptografii                                                      | Typowe zastosowanie                                                 |
| -------- | --------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **TLS**  | Asymetryczna + symetryczna                                            | Bezpieczne połączenia sieciowe (HTTPS)                              |
| **SSH**  | Asymetryczna + symetryczna                                            | Zdalne logowanie i transfer plików (SFTP)                           |
| **PGP**  | Asymetryczna + symetryczna                                            | Szyfrowanie i podpisywanie e-maili                                  |
| **AES**  | Symetryczna                                                           | Szyfrowanie lokalnych danych i plików                               |
| **SNMP** | (Nie kryptograficzny sam w sobie, ale SNMPv3 ma opcje bezpieczeństwa) | Zarządzanie urządzeniami sieciowymi – nie jest tu właściwym wyborem |

***

✅ **Ostateczne dopasowanie:**

| Nr | Zastosowanie                       | Protokół |
| -- | ---------------------------------- | -------- |
| 1  | Web Server                         | **TLS**  |
| 2  | Remote Server Access               | **SSH**  |
| 3  | Email Encryption                   | **PGP**  |
| 4  | File Encryption on a Local Machine | **AES**  |
