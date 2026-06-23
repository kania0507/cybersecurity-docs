# Juicy Details (TryHackMe)

### Cel analizy

Celem zadania jest odtworzenie działań atakującego na podstawie logów serwera WWW, logów SSH oraz FTP. Zamiast szukać pojedynczych wskaźników kompromitacji (IoC), analizujemy cały przebieg incydentu – od rozpoznania po uzyskanie dostępu do systemu

## Etap 1 – Rekonesans (Reconnaissance)

Atakujący rozpoczął od rozpoznania aplikacji.

Pierwszym narzędziem był:

* **Nmap**

Jego celem było:

* wykrycie dostępnych usług,
* sprawdzenie otwartych portów,
* zebranie informacji o środowisku.

Na tym etapie napastnik jeszcze niczego nie atakuje – poznaje powierzchnię ataku.

## Etap 2 – Enumeracja aplikacji

Po zidentyfikowaniu serwera WWW rozpoczęło się wyszukiwanie dostępnych zasobów.

Do tego wykorzystano:

* **Feroxbuster**

Narzędzie automatycznie wyszukuje:

* ukryte katalogi,
* endpointy API,
* panele administracyjne,
* pliki kopii zapasowych.

Dzięki temu atakujący lepiej poznał strukturę aplikacji.

## Etap 3 – Atak brute force

Następnie rozpoczęto próbę przejęcia kont użytkowników.

Wykorzystane narzędzie:

* **Hydra**

Celem był endpoint logowania:

```
/rest/user/login
```

Hydra wykonywała dużą liczbę prób logowania różnymi hasłami.

Analiza logów pokazuje, że:

* przez pewien czas serwer zwracał odpowiedzi oznaczające nieudane logowanie,
* następnie pojawiła się odpowiedź świadcząca o poprawnym uwierzytelnieniu.

Oznacza to, że:

> Atak brute force zakończył się sukcesem.

To pierwszy moment, w którym napastnik uzyskał dostęp do legalnego konta.

## Etap 4 – SQL Injection

Posiadając już dostęp do aplikacji, napastnik rozpoczął poszukiwanie kolejnych podatności.

Do ataku wykorzystał:

* **sqlmap**

Atak skierowany był przeciwko endpointowi:

```
/rest/products/search
```

Podatnym parametrem był:

```
q
```

Sqlmap automatycznie testował wiele payloadów SQL Injection.

Rezultat:

z bazy danych udało się odczytać m.in.

* adresy e-mail,
* hasła użytkowników.

To klasyczny przykład eskalacji informacji po uzyskaniu pierwszego dostępu.

## Etap 5 – Zbieranie danych (Data Discovery)

Napastnik nie zakończył działań na bazie danych.

Kolejnym celem było znalezienie plików pozostawionych na serwerze.

W logach pojawiają się próby dostępu do:

```
/ftp
```

To sugeruje, że atakujący szukał:

* kopii zapasowych,
* plików konfiguracyjnych,
* archiwów.

Takie katalogi bardzo często zawierają dane ułatwiające dalszy atak.

## Etap 6 – Dostęp do FTP

Analiza logów FTP pokazuje, że wykorzystano usługę:

```
FTP
```

oraz konto:

```
anonymous
```

To bardzo ważna obserwacja.

Oznacza to, że:

* anonimowy dostęp do FTP był włączony,
* nie wymagał podania hasła.

Napastnik próbował pobrać m.in.:

* kopie zapasowe,
* pliki konfiguracyjne.

Takie dane często zawierają:

* hasła,
* nazwy użytkowników,
* informacje o systemie.

## Etap 7 – Wykorzystanie zdobytych danych

Po zebraniu informacji napastnik przeszedł do kolejnego etapu.

W logach systemowych pojawia się logowanie przez:

```
SSH
```

na konto:

```
www-data
```

Oznacza to, że wcześniej zdobyte dane (np. hasło z SQL Injection lub z plików backupu) zostały wykorzystane do uzyskania dostępu do systemu operacyjnego.

To już nie jest atak na aplikację.

To pełny dostęp do serwera przez SSH.



## Jak wyglądał cały łańcuch ataku?

```
Recon (Nmap)        │        ▼Enumeracja aplikacji (Feroxbuster)        │        ▼Brute Force (Hydra)        │        ▼Uzyskanie poprawnego logowania        │        ▼SQL Injection (sqlmap)        │        ▼Wykradzenie danych użytkowników        │        ▼Dostęp do FTP        │        ▼Pobranie backupów        │        ▼Logowanie przez SSH        │        ▼Uzyskanie dostępu do systemu
```

## Co zrobił atakujący dobrze?

Napastnik nie korzystał z jednej podatności.

Zamiast tego połączył kilka technik:

1. rozpoznanie infrastruktury,
2. enumerację aplikacji,
3. brute force,
4. SQL Injection,
5. przeszukiwanie serwera FTP,
6. wykorzystanie zdobytych danych do logowania SSH.

Tak właśnie wygląda większość rzeczywistych incydentów – pojedyncza podatność rzadko prowadzi do pełnego przejęcia systemu. Znacznie częściej atakujący łączy kilka pozornie niewielkich błędów w jeden skuteczny łańcuch ataku (attack chain).

## Wnioski dla zespołu bezpieczeństwa

Analiza logów pokazuje kilka słabych punktów środowiska:

* brak skutecznej ochrony przed brute force,
* podatność na SQL Injection,
* włączony anonimowy dostęp do FTP,
* pozostawione pliki backupów,
* możliwość logowania przez SSH na konto techniczne (`www-data`),
* brak wykrycia nietypowej sekwencji działań wykonywanych przez jednego użytkownika.

Najcenniejszym elementem tego zadania nie jest odnalezienie odpowiedzi na pytania, ale zrozumienie sposobu działania napastnika.

Atakujący nie przejął serwera jednym narzędziem. Każdy kolejny krok wynikał z informacji zdobytych wcześniej:

* najpierw poznał środowisko,
* potem odnalazł podatne punkty,
* zdobył pierwsze konto,
* wykradł kolejne dane,
* wykorzystał je do dalszej eskalacji uprawnień,
* ostatecznie uzyskał dostęp do systemu przez SSH.

To klasyczny przykład **wieloetapowego ataku (multi-stage attack)**, w którym każda faza przygotowuje grunt pod następną. Z punktu widzenia analityka SOC kluczowe jest nie tylko wykrywanie pojedynczych zdarzeń, ale przede wszystkim ich korelowanie w jeden spójny scenariusz ataku.

**Juicy Details** jest dobrym przykładem pokazującym, jak pojedyncze zdarzenia z logów układają się w techniki z **MITRE ATT\&CK**. Nie wszystkie techniki są potwierdzone w 100% (analizujemy logi, a nie pamięć czy EDR), więc należy rozróżnić to, co **potwierdzone**, od tego, co **wnioskowane**.

Poniżej mapowanie.

| Etap ataku                               | Technika MITRE ATT\&CK                                                  | ID                                   |
| ---------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------ |
| Skanowanie portów (Nmap)                 | Active Scanning                                                         | **T1595**                            |
| Enumeracja katalogów (Feroxbuster)       | Gather Victim Host Information / Active Scanning (enumeracja aplikacji) | **T1595**                            |
| Atak brute force na logowanie            | Brute Force                                                             | **T1110**                            |
| Uzyskanie dostępu do aplikacji           | Valid Accounts                                                          | **T1078**                            |
| SQL Injection                            | Exploit Public-Facing Application                                       | **T1190**                            |
| Odczyt danych z bazy                     | Data from Information Repositories                                      | **T1213**                            |
| Dostęp do FTP                            | File and Directory Discovery (w kontekście przeglądania zasobów)        | **T1083**                            |
| Pobieranie backupów                      | Archive Collected Data / Data Staged (zależnie od interpretacji)        | **T1074**                            |
| Logowanie przez SSH                      | Remote Services (SSH)                                                   | **T1021.004**                        |
| Wykorzystanie zdobytych danych logowania | Valid Accounts                                                          | <p></p><p><strong>T1078</strong></p> |

### Przebieg ataku według taktyk MITRE ATT\&CK

#### 1. Reconnaissance

**T1595 – Active Scanning**

Atakujący rozpoczął od skanowania serwera przy użyciu **Nmap**, aby poznać dostępne usługi i otwarte porty.

#### 2. Initial Access

**T1190 – Exploit Public-Facing Application**

Aplikacja webowa została zaatakowana przy użyciu **SQL Injection**, co umożliwiło odczyt danych z bazy.

lub

**T1110 – Brute Force**

Równolegle napastnik przeprowadził atak słownikowy przy użyciu **Hydry**, aż uzyskał poprawne dane logowania.

#### 3. Credential Access

**T1110 – Brute Force**

Hasło zostało odgadnięte metodą brute force.

**T1078 – Valid Accounts**

Po zdobyciu poprawnych poświadczeń napastnik zaczął korzystać z legalnego konta użytkownika.

#### 4. Discovery

**T1083 – File and Directory Discovery**

Przeglądanie katalogów FTP oraz wyszukiwanie backupów i plików konfiguracyjnych.

#### 5. Collection

**T1213 – Data from Information Repositories**

Wyciągnięcie danych z bazy:

* kont użytkowników,
* adresów e-mail,
* haseł.

#### 6. Lateral Movement / Remote Access

**T1021.004 – SSH**

Po zdobyciu danych logowania nastąpiło zalogowanie do systemu przez SSH.

### Co jest najważniejsze?

Warto zauważyć, że **atakujący nie wykorzystał jednej podatności**, lecz połączył kilka technik ATT\&CK:

```
Reconnaissance(T1595)      │      ▼Brute Force(T1110)      │      ▼Valid Accounts(T1078)      │      ▼Exploit Public-Facing Application(T1190)      │      ▼Data from Information Repositories(T1213)      │      ▼File and Directory Discovery(T1083)      │      ▼Remote Services - SSH(T1021.004)

```

#### Uwaga metodologiczna

Jedna rzecz wymaga ostrożności: **Feroxbuster** nie ma dedykowanej techniki ATT\&CK opisującej "brute-force katalogów". W praktyce mapuje się go najczęściej do **T1595 – Active Scanning**, ponieważ służy do aktywnego rozpoznania aplikacji webowej. Nie należy na siłę przypisywać mu bardziej szczegółowej techniki, jeśli analiza logów tego nie potwierdza.

Taki sposób mapowania jest zgodny z praktyką stosowaną przez analityków SOC i zespoły Threat Intelligence: przypisuje się wyłącznie techniki, które znajdują potwierdzenie w dostępnych artefaktach, unikając nadinterpretacji.

**Feroxbuster** to narzędzie do **automatycznej enumeracji zawartości serwera WWW**. Jego zadaniem jest odnalezienie zasobów, które nie są widoczne z poziomu zwykłej nawigacji po stronie.

Najprościej można powiedzieć:

> **Feroxbuster zgaduje nazwy katalogów i plików na serwerze, wysyłając tysiące żądań HTTP.**

[https://tryhackme.com/room/juicydetails](https://tryhackme.com/room/juicydetails)&#x20;
