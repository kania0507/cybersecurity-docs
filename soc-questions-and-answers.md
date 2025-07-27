# SOC - questions & answers

**BASICS**

***

### 1. Podstawowa znajomość konfiguracji i administracji systemami operacyjnymi Linux i Windows

#### Linux – co powinnaś umieć i co to oznacza?

* **Podstawowe komendy w terminalu:**\
  Linux to system oparty na wierszu poleceń, więc musisz znać komendy takie jak:
  * `ls` – wyświetla zawartość katalogu, czyli listę plików i folderów,
  * `cd` – zmienia katalog, w którym aktualnie pracujesz,
  * `cat` – wyświetla zawartość pliku,
  * `grep` – wyszukuje w tekście, np. w logach, konkretne słowa lub frazy,
  * `chmod` – zmienia uprawnienia do plików i folderów (np. kto może je czytać lub modyfikować),
  * `ps`, `top` – pokazują uruchomione procesy i obciążenie systemu,
  * `netstat` lub `ss` – pokazują aktywne połączenia sieciowe.\
    To są narzędzia do codziennej pracy i diagnozy.
* **Zarządzanie użytkownikami i grupami:**\
  System Linux pozwala tworzyć różne konta użytkowników, by kontrolować dostęp do zasobów.
  * `adduser` tworzy nowego użytkownika,
  * `passwd` zmienia hasło,
  * `groups` pokazuje, do jakich grup należy użytkownik (grupy decydują o prawach dostępu).\
    Znajomość tego pozwala Ci nadawać uprawnienia i zabezpieczać system.
* **Usługi (daemony):**\
  Usługi to programy działające w tle, które wykonują określone zadania (np. serwer SSH, który pozwala zdalnie się łączyć).
  * W Linuxie zarządza się nimi za pomocą `systemctl` (np. `systemctl start sshd` uruchamia serwer SSH).\
    Usługi muszą być włączone, aby działały, a czasem trzeba je zrestartować, gdy coś nie działa.
* **Logi systemowe:**\
  Systemy zapisują informacje o tym, co się dzieje, do plików zwanych logami.
  * W Linuxie są one zwykle w `/var/log/` (np. `auth.log` zawiera informacje o logowaniach).\
    Umiejętność czytania logów pozwala zrozumieć, czy np. ktoś próbował się włamać.

***

#### Windows – co powinnaś umieć i co to oznacza?

* **Wiersz poleceń (cmd) i PowerShell:**\
  Podobnie jak Linux, Windows ma narzędzia tekstowe do zarządzania systemem.
  * `ipconfig` – pokazuje konfigurację sieci,
  * `netstat` – pokazuje aktywne połączenia,
  * `tasklist` – listuje uruchomione procesy,
  * `Get-Service` – pokazuje działające usługi.\
    Znajomość tych poleceń ułatwia diagnozowanie problemów.
* **Zarządzanie użytkownikami:**\
  Możesz dodawać i usuwać konta przez GUI lub komendy `net user`.\
  Kontrola użytkowników to podstawa bezpieczeństwa.
* **Usługi w Windows:**\
  Usługi (services) to programy działające w tle, np. Windows Update lub serwer drukarki.
  * Można nimi zarządzać z poziomu `services.msc` (graficznego panelu) albo PowerShell (`Start-Service`, `Stop-Service`).\
    Usługi muszą być włączone, aby odpowiednie funkcje działały.
* **Event Viewer:**\
  To narzędzie do przeglądania logów systemowych (zapisuje się tam np. kto się logował, błędy systemowe, alerty bezpieczeństwa).

***

### 2. Podstawowa znajomość narzędzi typu SIEM (Splunk, Elasticsearch)

* **Co to jest SIEM?**\
  To narzędzie do zbierania i analizy logów z różnych źródeł (serwery, firewalle, aplikacje) w jednym miejscu. Pozwala wykrywać incydenty bezpieczeństwa.
* **Splunk i Elasticsearch:**
  * Splunk ma własny język zapytań (SPL), dzięki któremu możesz np. znaleźć wszystkie próby nieudanych logowań:\
    `index=windows EventCode=4625`
  * Elasticsearch używa zapytań w formacie Lucene lub JSON.\
    Umiejętność filtrowania logów to podstawa pracy analityka bezpieczeństwa.
* **Dlaczego to ważne?**\
  Przeszukiwanie dziesiątek tysięcy logów ręcznie jest niemożliwe – SIEM robi to za Ciebie i pozwala szybko reagować.

***

### 3. Podstawowa wiedza o modelu TCP/IP i protokołach (HTTP, SSH, SMTP, DNS, NTP, LDAP)

#### Model TCP/IP i różnica TCP vs UDP

* **Model TCP/IP** opisuje, jak komputery komunikują się przez sieć, podzielony na warstwy:
  * Warstwa sieciowa – zarządza adresami IP i routingiem,
  * Warstwa transportowa – zapewnia przesyłanie danych (np. TCP, UDP),
  * Warstwa aplikacji – protokoły takie jak HTTP, SMTP.
* **Różnica TCP a UDP:**
  * **TCP (Transmission Control Protocol)** – protokół „połączeniowy”: zanim dane zostaną wysłane, nawiązuje połączenie, sprawdza, czy wszystko dotarło poprawnie, i jeśli trzeba, wysyła ponownie. Jest wolniejszy, ale bezpieczny (np. HTTP, FTP).
  * **UDP (User Datagram Protocol)** – protokół bez połączenia: wysyła dane „na ślepo”, nie czeka na potwierdzenie. Jest szybszy, ale mniej niezawodny (np. transmisja audio, wideo).

#### Co to jest podstawowy routing?

* Routing to sposób, w jaki pakiety danych docierają z Twojego komputera do innego urządzenia w sieci (np. strony internetowej).
* Podstawowy routing oznacza, że znasz działanie routerów i potrafisz sprawdzić trasę pakietu (np. komenda `traceroute` lub `tracert`), czyli jak dane „skaczą” przez różne urządzenia aż do celu.

***

#### Protokół HTTP

* Służy do przesyłania stron internetowych.
* Znajomość metod:
  * **GET** – pobiera dane ze strony,
  * **POST** – wysyła dane na serwer (np. formularz).
* Kody statusu HTTP informują, co się stało:
  * `200 OK` – wszystko dobrze,
  * `404 Not Found` – strona nie znaleziona,
  * `500 Internal Server Error` – błąd serwera.

***

#### Protokół SSH i klucze publiczne/prywatne

* **SSH (Secure Shell)** to protokół pozwalający na bezpieczne, zaszyfrowane połączenie zdalne do serwera.
* **Klucze prywatne i publiczne:**
  * Klucz **publiczny** jest jak adres e-mail – możesz go udostępniać.
  * Klucz **prywatny** to tajny kod, który trzymasz tylko dla siebie.
  * Połączenie działa tak, że serwer ma Twój klucz publiczny i może sprawdzić, czy osoba łącząca się ma odpowiadający mu klucz prywatny. Dzięki temu nikt niepowołany nie może się zalogować bez klucza prywatnego, nawet jeśli zna login.
  * To znacznie bezpieczniejsze niż logowanie hasłem.

***

#### SMTP

* Protokół do wysyłania maili.
* Porty:
  * 25 – podstawowy port SMTP, często blokowany przez ISP,
  * 587 – port do wysyłania maili z uwierzytelnieniem (najczęściej używany),
  * 465 – SMTP przez SSL (szyfrowane).
* SMTP pozwala serwerom pocztowym wymieniać wiadomości.

***

#### DNS

* System tłumaczący nazwy domen na adresy IP (np. `google.com` → `142.250.190.14`).
* Komendy:
  * `nslookup` lub `dig` – pozwalają sprawdzić, jaki adres IP odpowiada nazwie.
* Znajomość rekordów DNS:
  * `A` – adres IP,
  * `MX` – serwery pocztowe,
  * `CNAME` – alias nazwy,
  * `TXT` – tekstowe informacje, często wykorzystywane do weryfikacji domeny lub SPF.

***

#### NTP

* **Network Time Protocol** – protokół synchronizujący zegary komputerów w sieci.
* Poprawny czas jest krytyczny, bo:
  * Logi muszą mieć poprawne znaczniki czasu, aby można było analizować zdarzenia,
  * Certyfikaty SSL i inne mechanizmy bezpieczeństwa działają na bazie czasu.

***

#### LDAP

* **Lightweight Directory Access Protocol** to protokół do zarządzania informacjami o użytkownikach i urządzeniach w sieci, np. w Active Directory.
* Umożliwia uwierzytelnianie i autoryzację użytkowników.
* Port 389 – standardowy port LDAP, 636 – LDAP przez SSL.
* Dzięki LDAP użytkownicy mogą logować się do różnych systemów firmowych na podstawie jednej bazy danych.

***

#### Podsumowanie

* **Znajomość systemów Linux i Windows** pozwoli Ci samodzielnie wykonywać podstawową administrację i diagnozę problemów.
* **SIEM** to narzędzie niezbędne do analizy dużych ilości logów i szybkiego wykrywania zagrożeń.
* **Protokoły sieciowe i model TCP/IP** to fundament rozumienia, jak działa internet i sieć firmowa oraz jak rozpoznawać zagrożenia.

***

