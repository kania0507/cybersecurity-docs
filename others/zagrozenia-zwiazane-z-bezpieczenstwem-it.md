# Zagrożenia związane z bezpieczeństwem IT

### 1. **Zagrożenia dotyczące ludzi (czynnika ludzkiego)**

To najczęstsze źródło incydentów — człowiek bywa najsłabszym ogniwem.

| Zagrożenie                             | Opis                                                                                             |
| -------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Phishing / spear phishing**          | Podszywanie się pod znane osoby lub instytucje w celu wyłudzenia danych logowania lub pieniędzy. |
| **Spoofing / impersonacja**            | Fałszywe e-maile, numery telefonów, domeny – mają wyglądać jak prawdziwe.                        |
| **Socjotechnika (social engineering)** | Manipulacja psychologiczna – np. „pomoc techniczna” prosi o hasło.                               |
| **Brak świadomości użytkowników**      | Klikanie w linki, instalowanie nieznanych aplikacji, słabe hasła.                                |
| **Shadow IT**                          | Używanie prywatnych kont/aplikacji do pracy bez zgody IT, co tworzy luki w bezpieczeństwie.      |

***

### 2. **Zagrożenia techniczne (systemowe / aplikacyjne)**

| Zagrożenie                                               | Opis                                                                                          |
| -------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Malware (złośliwe oprogramowanie)**                    | Ogólna kategoria – wirusy, trojany, spyware, keyloggery, rootkity itp.                        |
| **Ransomware**                                           | Złośliwe oprogramowanie szyfrujące dane i żądające okupu za ich odszyfrowanie.                |
| **Wirusy i robaki**                                      | Samoreplikujące się programy infekujące systemy lub sieci.                                    |
| **Backdoory**                                            | Ukryte mechanizmy pozwalające atakującemu uzyskać dostęp do systemu.                          |
| **Exploit / zero-day**                                   | Wykorzystanie nieznanej (lub niezałatanej) podatności w systemie lub aplikacji.               |
| **SQL Injection / XSS / CSRF**                           | Wstrzyknięcia kodu w aplikacjach webowych – prowadzą do kradzieży danych lub przejęcia sesji. |
| **Brak aktualizacji oprogramowania (patch management)**  | Pozostawienie luk w systemach, które mogą być łatwo wykorzystane.                             |
| **Niepoprawna konfiguracja serwerów (misconfiguration)** | Otwarte porty, domyślne hasła, brak szyfrowania, zły CORS lub CSP.                            |
| **Ataki DoS / DDoS**                                     | Przeciążenie serwera ogromną liczbą zapytań, aż przestanie działać.                           |
| **Man-in-the-Middle (MITM)**                             | Podsłuchiwanie lub modyfikacja ruchu między użytkownikiem a serwerem.                         |
| **Brak szyfrowania (HTTP zamiast HTTPS)**                | Dane przesyłane jawnym tekstem mogą zostać przechwycone.                                      |
| **Supply Chain Attack**                                  | Wstrzyknięcie złośliwego kodu do zaufanych komponentów (np. bibliotek, CDN).                  |

***

### 3. **Zagrożenia sieciowe**

| Zagrożenie                        | Opis                                                           |
| --------------------------------- | -------------------------------------------------------------- |
| **ARP spoofing / poisoning**      | Podszywanie się pod urządzenia w sieci lokalnej.               |
| **DNS poisoning / hijacking**     | Przekierowanie ruchu na fałszywe strony.                       |
| **Eavesdropping / sniffing**      | Podsłuchiwanie ruchu sieciowego (np. przez Wi-Fi).             |
| **Brak segmentacji sieci**        | Ułatwia rozprzestrzenianie się ataków w całej infrastrukturze. |
| **Brak firewalli lub złe reguły** | Pozwala na nieautoryzowany dostęp z zewnątrz.                  |

***

### 4. **Zagrożenia związane z danymi**

| Zagrożenie                                         | Opis                                                                     |
| -------------------------------------------------- | ------------------------------------------------------------------------ |
| **Wycieki danych (data breach)**                   | Upublicznienie lub kradzież poufnych informacji (np. klientów).          |
| **Nieuprawniony dostęp / brak kontroli uprawnień** | Użytkownicy mają zbyt szerokie uprawnienia.                              |
| **Brak szyfrowania danych w spoczynku**            | Dane na dysku lub w bazie są zapisane w postaci jawnej.                  |
| **Brak kopii zapasowych lub błędy w backupie**     | Uniemożliwia odzyskanie danych po awarii lub ataku.                      |
| **Przechowywanie haseł w postaci jawnej**          | Krytyczny błąd bezpieczeństwa – umożliwia natychmiastowy dostęp do kont. |

***

### 5. **Zagrożenia organizacyjne**

| Zagrożenie                                   | Opis                                                             |
| -------------------------------------------- | ---------------------------------------------------------------- |
| **Brak polityk bezpieczeństwa**              | Brak formalnych zasad dotyczących haseł, dostępów, aktualizacji. |
| **Brak planu reagowania na incydenty (IRP)** | Organizacja nie wie, co robić po wykryciu ataku.                 |
| **Brak kopii zapasowych / testów DR**        | Nieprzygotowanie na awarie i ransomware.                         |
| **Naruszenia RODO / GDPR**                   | Przechowywanie lub przetwarzanie danych bez podstawy prawnej.    |
| **Brak audytów i testów penetracyjnych**     | Niezauważone podatności przez lata.                              |

***

### 6. **Zagrożenia mobilne i IoT**

| Zagrożenie                                           | Opis                                                                                     |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Złośliwe aplikacje mobilne**                       | Wyłudzają dane, podsłuchują rozmowy, zbierają lokalizację.                               |
| **Brak aktualizacji systemu Android/iOS**            | Pozostawia znane luki otwarte.                                                           |
| **Bluejacking / Bluesnarfing / Bluebugging**         | Ataki przez Bluetooth.                                                                   |
| **IoT bez zabezpieczeń (kamery, routery, czujniki)** | Często brak hasła, HTTPS lub aktualizacji — podatne na przejęcie i włączenie do botnetu. |

***

### &#x20;7. **Zagrożenia wewnętrzne (insider threats)**

| Zagrożenie                                       | Opis                                                                      |
| ------------------------------------------------ | ------------------------------------------------------------------------- |
| **Nieuczciwy pracownik / sabotaż**               | Celowe usunięcie danych, wyciek lub uszkodzenie systemu.                  |
| **Nieumyślne błędy pracowników**                 | Wysłanie pliku do niewłaściwego odbiorcy, kliknięcie linku phishingowego. |
| **Brak kontroli dostępu po odejściu pracownika** | Konto nadal aktywne po zwolnieniu – ryzyko nadużycia.                     |

***

### 8. **Zagrożenia wynikające z błędów w procesach IT**

| Zagrożenie                                                     | Opis                                              |
| -------------------------------------------------------------- | ------------------------------------------------- |
| **Brak testów bezpieczeństwa przed wdrożeniem**                | Aplikacja produkcyjna zawiera błędy.              |
| **Niepoprawne zarządzanie tajnymi danymi (secret management)** | Klucze API, hasła w repozytoriach GitHub.         |
| **Brak kontroli wersji i CI/CD zabezpieczeń**                  | Wprowadzenie luk przy automatycznych wdrożeniach. |
| **Nieprawidłowe logowanie i monitoring**                       | Atak zostaje niezauważony przez długi czas.       |

***

### 9. **Zagrożenia związane z chmurą (Cloud Security)**

| Zagrożenie                                               | Opis                                                         |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| **Publiczne zasoby (np. otwarte S3 bucket)**             | Dane dostępne publicznie przez błąd konfiguracji.            |
| **Błędne role IAM**                                      | Zbyt szerokie uprawnienia użytkowników lub aplikacji.        |
| **Brak szyfrowania danych w chmurze**                    | Dane mogą zostać przechwycone przez dostawcę lub napastnika. |
| **Ataki na API chmurowe**                                | Brak rate limiting, brak autoryzacji.                        |
| **Zależność od zewnętrznych dostawców (vendor lock-in)** | Utrudnia szybką reakcję w razie incydentu.                   |

***

### 10. **Podsumowanie – grupy ryzyka**

| Kategoria        | Przykłady zagrożeń                                     |
| ---------------- | ------------------------------------------------------ |
| **Ludzie**       | Phishing, socjotechnika, błędy użytkowników            |
| **Systemy**      | Malware, ransomware, exploit, XSS                      |
| **Sieć**         | MITM, DDoS, spoofing                                   |
| **Dane**         | Wycieki, brak szyfrowania, złe backupy                 |
| **Organizacja**  | Brak polityk, audytów, IRP                             |
| **Chmura / IoT** | Błędne konfiguracje, brak aktualizacji, publiczne dane |

### **11. (Dodatkowy punkt) — Zagrożenia związane z bazami danych**

| Zagrożenie                                  | Opis                                                                    | Skutki                                                    | Sposoby ochrony                                                                                      |
| ------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **SQL Injection**                           | Wstrzyknięcie kodu SQL przez pola formularzy lub parametry URL          | Kradzież, modyfikacja lub usunięcie danych                | Używaj _parametryzowanych zapytań_, ORM, walidacji danych wejściowych, ogranicz uprawnienia konta DB |
| **Brak szyfrowania danych w bazie**         | Dane (np. hasła, numery PESEL) przechowywane w postaci jawnej           | Ujawnienie danych w razie wycieku lub backupu             | Szyfruj dane w spoczynku (_at rest encryption_) i połączenia (_TLS in transit_)                      |
| **Hasła zapisane w postaci jawnej**         | Brak funkcji hashujących                                                | Natychmiastowy dostęp do kont użytkowników po wycieku     | Stosuj `bcrypt`, `Argon2`, `PBKDF2` z solą                                                           |
| **Niepoprawne uprawnienia użytkowników**    | Aplikacja lub użytkownik ma pełne prawa `DBA` lub `root`                | Łatwe przejęcie całej bazy przy błędzie w aplikacji       | Zasada minimalnych uprawnień (least privilege) – osobne konta dla aplikacji i admina                 |
| **Brak kontroli dostępu / audytu**          | Nie ma logów, kto i kiedy miał dostęp do danych                         | Niemożność wykrycia nadużyć / wycieku                     | Włącz logowanie zapytań i audyt bezpieczeństwa (np. PostgreSQL `pg_audit`)                           |
| **Brak aktualizacji silnika bazy danych**   | Niezałatane luki w MySQL, PostgreSQL, MongoDB itd.                      | Możliwe exploit’y zdalne i eskalacja uprawnień            | Regularne patchowanie i aktualizacje                                                                 |
| **Zdalny dostęp bez zabezpieczenia**        | Otwarty port DB (np. 3306, 5432) publicznie                             | Ataki brute-force lub przejęcie bazy                      | Blokuj zdalny dostęp, stosuj VPN/firewall, ogranicz IP                                               |
| **Niepoprawne kopie zapasowe (backupy)**    | Backupy przechowywane w chmurze bez szyfrowania lub dostępne publicznie | Wycieki danych klientów                                   | Szyfruj i kontroluj dostęp do backupów, regularnie testuj przywracanie                               |
| **Błędna konfiguracja / domyślne konta**    | Pozostawione `root`/`admin` bez hasła, testowe bazy                     | Natychmiastowy dostęp dla atakującego                     | Usuń konta domyślne, zmień porty, stosuj silne hasła                                                 |
| **Brak ograniczeń zapytań (rate limiting)** | Użytkownik może wykonywać tysiące zapytań naraz                         | Denial of Service lub ujawnienie danych przez brute-force | Limituj zapytania i włącz monitoring                                                                 |
| **Eksfiltracja danych przez błędne API**    | Endpointy zwracają za dużo danych z bazy                                | Wycieki danych wrażliwych                                 | Filtruj dane po stronie backendu, waliduj zapytania i odpowiedzi                                     |



***

### **Dobre praktyki ochrony baz danych**

1. **Zasada najmniejszych uprawnień** – każda aplikacja powinna mieć tylko to, co niezbędne (np. SELECT/INSERT, bez DROP).
2. **Szyfrowanie** – zarówno połączenia (TLS), jak i dane w bazie (TDE, kolumny wrażliwe).
3. **Hashowanie haseł** – `bcrypt`, `Argon2id`, `PBKDF2`.
4. **Regularne aktualizacje** – zarówno silnika DB, jak i bibliotek łączących.
5. **Audyt i logowanie** – monitoruj kto, kiedy i jakie zapytania wykonuje.
6. **Backupy** – szyfrowane, przetestowane, przechowywane bez dostępu publicznego.
7. **Segmentacja sieci** – serwer baz danych nie powinien być dostępny bezpośrednio z internetu.
8. **Monitorowanie i alerty** – narzędzia typu _Database Activity Monitoring (DAM)_, SIEM, alerty bezpieczeństwa.
9. **Testy bezpieczeństwa aplikacji (pentesty)** – regularnie sprawdzaj podatności typu SQL Injection.
10. **Polityki haseł i rotacja kluczy** – wymuszaj mocne hasła, stosuj uwierzytelnianie wieloskładnikowe (MFA).

