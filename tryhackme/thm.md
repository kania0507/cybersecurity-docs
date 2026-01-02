---
description: Notatki z TryHackMe
---

# All notes

```
Gobuster to narzędzie programowe do brutalnego wymuszania katalogów na serwerach WWW 
gobuster -u http://fakebank.thm -w wordlist.txt dir
```

<br>

<br>

Do zadań związanych z bezpieczeństwem obronnym zalicza się m.in.:

* Świadomość użytkowników w zakresie cyberbezpieczeństwa: Szkolenie użytkowników w zakresie cyberbezpieczeństwa pomaga chronić ich systemy przed atakami.
* Dokumentowanie i zarządzanie aktywami: Musimy wiedzieć, jakimi systemami i urządzeniami musimy odpowiednio zarządzać i które musimy chronić.
* Aktualizowanie i łatanie systemów: dbanie o to, aby komputery, serwery i urządzenia sieciowe były prawidłowo aktualizowane i zabezpieczane przed wszelkimi znanymi lukami w zabezpieczeniach (słabościami).
* Konfigurowanie urządzeń zabezpieczających zapobiegawczo: zapory sieciowe i systemy zapobiegania włamaniom ( IPS ) są krytycznymi składnikami zabezpieczeń zapobiegawczych. Zapory sieciowe kontrolują, jaki ruch sieciowy może wejść do systemu lub sieci, a jaki może go opuścić. IPS blokuje cały ruch sieciowy, który pasuje do obecnych reguł i sygnatur ataków.
* Konfigurowanie urządzeń rejestrujących i monitorujących: Prawidłowe rejestrowanie i monitorowanie sieci są niezbędne do wykrywania złośliwych działań i włamań. Jeśli w naszej sieci pojawi się nowe nieautoryzowane urządzenie, powinniśmy być w stanie je wykryć.

<br>

<br>

Security _Operations Center_ ( SOC ) to zespół specjalistów od cyberbezpieczeństwa, który monitoruje sieć i jej systemy w celu wykrywania złośliwych zdarzeń cyberbezpieczeństwa. Niektóre z głównych obszarów zainteresowania SOC to:

* Luki: Za każdym razem, gdy zostanie odkryta luka w systemie (słabość), konieczne jest jej naprawienie poprzez zainstalowanie odpowiedniej aktualizacji lub poprawki. Gdy poprawka jest niedostępna, należy podjąć niezbędne środki, aby uniemożliwić atakującemu jej wykorzystanie. Chociaż naprawa luk jest kluczowa dla SOC , nie jest ona koniecznie do nich przypisana.
* Naruszenia zasad: Zasady bezpieczeństwa to zbiór reguł wymaganych do ochrony sieci i systemów. Na przykład naruszeniem zasad może być przesłanie przez użytkowników poufnych danych firmy do usługi przechowywania danych online.
* Nieautoryzowana aktywność: Rozważ przypadek, w którym nazwa użytkownika i hasło zostały skradzione, a atakujący używa ich do zalogowania się do sieci. SOC musi wykryć i zablokować takie zdarzenie tak szybko, jak to możliwe, zanim nastąpią dalsze szkody.
* Włamania do sieci: Bez względu na to, jak dobre jest Twoje bezpieczeństwo, zawsze istnieje ryzyko włamania. Włamanie może nastąpić, gdy użytkownik kliknie złośliwy link lub gdy atakujący wykorzysta publiczny serwer. Tak czy inaczej, gdy dochodzi do włamania, musimy wykryć je tak szybko, jak to możliwe, aby zapobiec dalszym szkodom.

Operacje bezpieczeństwa obejmują różne zadania mające na celu zapewnienie ochrony; jednym z takich zadań jest wykrywanie zagrożeń.

<br>

<br>

<br>

Cztery główne fazy procesu reagowania na incydenty to:

1. Przygotowanie: Wymaga to przeszkolonego i gotowego do obsługi incydentów zespołu. W idealnym przypadku wdrażane są różne środki, aby zapobiec wystąpieniu incydentów.
2. Wykrywanie i analiza: Zespół dysponuje zasobami niezbędnymi do wykrycia każdego incydentu. Co więcej, niezwykle istotne jest dalsze analizowanie każdego wykrytego incydentu w celu określenia jego powagi.
3. Ograniczenie, eliminacja i odzyskiwanie: Po wykryciu incydentu kluczowe jest powstrzymanie go przed wpływem na inne systemy, wyeliminowanie go i odzyskanie dotkniętych nim systemów. Na przykład, gdy zauważymy, że system jest zainfekowany wirusem komputerowym, chcielibyśmy powstrzymać (ograniczyć) rozprzestrzenianie się wirusa na inne systemy, oczyścić (wyeliminować) wirusa i zapewnić prawidłowe odzyskiwanie systemu.
4. Działania poincydentalne: Po pomyślnym odzyskaniu danych sporządzany jest raport, a wyciągnięte wnioski są udostępniane w celu zapobiegania podobnym incydentom w przyszłości.

<br>

#### Kryminalistyka cyfrowa i reagowanie na incydenty ( DFIR )

<br>

<br>

<br>

<br>

<br>

<br>

**Analiza złośliwego oprogramowania**

Malware oznacza malware software. _Oprogramowanie_ odnosi się do programów, dokumentów i plików, które można zapisać na dysku lub wysłać przez sieć. Malware obejmuje wiele typów, takich jak:

* Wirus to fragment kodu (część programu), który dołącza się do programu. Jest zaprojektowany tak, aby rozprzestrzeniać się z jednego komputera na drugi i działa poprzez zmienianie, nadpisywanie i usuwanie plików po zainfekowaniu komputera. Rezultatem jest spowolnienie komputera lub jego bezużyteczność.
* Trojan Horse to program, który pokazuje jedną pożądaną funkcję, ale ukrywa pod spodem złośliwą funkcję. Na przykład ofiara może pobrać odtwarzacz wideo z podejrzanej witryny, co daje atakującemu pełną kontrolę nad systemem.
* Ransomware to złośliwy program, który szyfruje pliki użytkownika. Szyfrowanie sprawia, że ​​pliki stają się nieczytelne bez znajomości hasła szyfrowania. Atakujący oferuje użytkownikowi hasło szyfrowania, jeśli użytkownik jest skłonny zapłacić „okup”.

<br>



<br>

Netstat in Linux to ss = socket statistics

netstat -lntu | grep 443

<br>

&#x20;Shodan jest prawdopodobnie najlepszą wyszukiwarką do znajdowania podatnych systemów na urządzeniach, które są publicznie wystawione i nie są chronione . Jest powszechnie używany przez agencje ścigania. Możesz go również użyć do znajdowania urządzeń, które niedawno zostały podłączone do Internetu.

Shodan działa poprzez skanowanie internetu w poszukiwaniu urządzeń podłączonych do sieci, zbierając dane takie jak adresy IP, banery usług, otwarte porty oraz inne szczegóły techniczne. Proces ten polega na regularnym przesyłaniu zapytań do urządzeń w celu uzyskania informacji o ich konfiguracji i stanie.

<br>

Censys zapewnia analitykom ds. bezpieczeństwa widoczność i kontekst w Internecie, których potrzebują, aby szybko wykrywać incydenty i na nie reagować, identyfikować zdarzenia nietypowe oraz ustalać priorytety działań naprawczych.

<br>

Shodan koncentruje się na urządzeniach i systemach podłączonych do Internetu, takich jak serwery, routery, kamery internetowe i urządzenia IoT. Censys z kolei koncentruje się na hostach podłączonych do Internetu, witrynach internetowych, certyfikatach i innych zasobach internetowych. Niektóre z jego przypadków użycia obejmują wyliczanie używanych domen, audytowanie otwartych portów i usług oraz wykrywanie nieuczciwych zasobów w sieci.

<br>

VirusTotal to internetowa witryna internetowa, która zapewnia usługę skanowania antywirusowego plików przy użyciu wielu silników antywirusowych. Umożliwia użytkownikom przesyłanie plików lub podawanie adresów URL w celu przeskanowania ich za pomocą wielu silników antywirusowych i skanerów witryn w jednej operacji. Mogą nawet wprowadzać skróty plików, aby sprawdzić wyniki wcześniej przesłanych plików.

<br>

Have I Been Pwned (HIBP) robi jedną rzecz; informuje, czy adres e-mail pojawił się w wycieku danych. Znalezienie czyjegoś adresu e-mail w wyciekłych danych wskazuje na wyciek prywatnych informacji i, co ważniejsze, haseł. Wielu użytkowników używa tego samego hasła na wielu platformach, jeśli jedna platforma zostanie naruszona, ich hasło na innych platformach również zostanie ujawnione. Rzeczywiście, hasła są zazwyczaj przechowywane w formacie zaszyfrowanym; jednak wiele haseł nie jest tak złożonych i można je odzyskać za pomocą różnych ataków

<br>

Możemy myśleć o programie Common Vulnerabilities and Exposures (CVE) jako o słowniku luk w zabezpieczeniach. Zapewnia on standaryzowany identyfikator luk w zabezpieczeniach i problemów bezpieczeństwa w produktach programowych i sprzętowych. Każdej luce w zabezpieczeniach przypisuje się identyfikator CVE o standaryzowanym formacie, takim jak CVE-2024-29988. Ten unikalny identyfikator (CVE ID) zapewnia, że ​​wszyscy, od badaczy bezpieczeństwa po dostawców i specjalistów IT, odnoszą się do tej samej luki w zabezpieczeniach, w tym przypadku CVE-2024-29988.

<br>

<br>

### Exploit Database – potrzebna zgoda

[https://www.exploit-db.com/](https://www.exploit-db.com/)

<br>

GitHub, oparta na sieci platforma do tworzenia oprogramowania, może zawierać wiele narzędzi związanych z CVE, wraz z kodami proof-of-concept (PoC) i exploit.

<br>

netstat \[-a] \[-b] \[-e] \[-n] \[-o] \[-p \<Protocol>] \[-r] \[-s] \[\<interval>]

-a Wyświetla wszystkie aktywne połączenia TCP oraz porty TCP i UDP, na których nasłuchuje komputer.\
-b Wyświetla plik wykonywalny zaangażowany w tworzenie każdego połączenia lub portu nasłuchującego. W niektórych przypadkach dobrze znane pliki wykonywalne hostują wiele niezależnych komponentów, a w takich przypadkach wyświetlana jest sekwencja komponentów zaangażowanych w tworzenie połączenia lub portu nasłuchującego. W takim przypadku nazwa pliku wykonywalnego znajduje się w \[] na dole, na górze jest wywołany przez niego komponent itd., aż do osiągnięcia TCP/IP. Należy pamiętać, że ta opcja może być czasochłonna i zakończy się niepowodzeniem, jeśli nie masz wystarczających uprawnień.\
-e Wyświetla statystyki Ethernet, takie jak liczba bajtów i pakietów wysłanych i odebranych. Ten parametr można łączyć z -s.\
-n Wyświetla aktywne połączenia TCP, jednak adresy i numery portów są wyrażane numerycznie i nie jest podejmowana próba określenia nazw.\
-o Wyświetla aktywne połączenia TCP i zawiera identyfikator procesu (PID) dla każdego połączenia. Aplikację można znaleźć na podstawie PID na karcie Procesy w Menedżerze zadań systemu Windows. Ten parametr można łączyć z parametrami -a, -n i -p.\
-p \<Protokół> Pokazuje połączenia dla protokołu określonego przez Protokół. W tym przypadku Protokół może być tcp, udp, tcpv6 lub udpv6. Jeśli ten parametr jest używany z parametrem -s w celu wyświetlenia statystyk według protokołu, Protokół może być tcp, udp, icmp, ip, tcpv6, udpv6, icmpv6 lub ipv6.\
-s Wyświetla statystyki według protokołu. Domyślnie statystyki są wyświetlane dla protokołów TCP, UDP, ICMP i IP. Jeśli protokół IPv6 jest zainstalowany, statystyki są wyświetlane dla protokołów TCP przez IPv6, UDP przez IPv6, ICMPv6 i IPv6. Parametr -p może być używany do określania zestawu protokołów.\
-r Wyświetla zawartość tabeli routingu IP. Jest to równoważne poleceniu route print.\
\<interval> Wyświetla ponownie wybrane informacje co interwał sekund. Naciśnij CTRL+C, aby zatrzymać ponowne wyświetlanie. Jeśli ten parametr zostanie pominięty, to polecenie wydrukuje wybrane informacje tylko raz.\
/? Wyświetla pomoc w wierszu poleceń<br>

<br>

<br>

<br>

<br>

LINUX FUNDAMENTALS

<br>

\> sudo apt update

\> whoami

\> cat file.txt

\> pwd – full path dir

\> find -name passwords.txt

find -name \*.txt

\> wc -l access.log

\> grep „81.143.211.90 ” access.log

<br>

& Ten operator umożliwia uruchamianie poleceń w tle terminala.\
&& Ten operator umożliwia łączenie wielu poleceń w jednym wierszu terminala.\
\> Ten operator jest przekierowaniem — oznacza to, że możemy pobrać dane wyjściowe z polecenia (takie jak użycie cat do wyprowadzenia pliku) i skierować je w inne miejsce.\
\>>\
Ten operator wykonuje tę samą funkcję co operator >, ale dołącza dane wyjściowe zamiast je zastępować (co oznacza, że ​​nic nie jest nadpisywane).

<br>

Echo hey > welcome

cat welcome

hey

<br>

echo hello » welcome

cat welcome

hey

hello

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

## Active Reconnaissance

<br>

Istnieje również wiele dodatków do przeglądarek Firefox i Chrome, które mogą pomóc w testach penetracyjnych. Oto kilka przykładów:\
\
FoxyProxy umożliwia szybką zmianę serwera proxy używanego do uzyskiwania dostępu do docelowej witryny. To rozszerzenie przeglądarki jest wygodne, gdy używasz narzędzia takiego jak Burp Suite lub gdy musisz regularnie zmieniać serwery proxy. Możesz pobrać FoxyProxy dla przeglądarki Firefox stąd.\
User-Agent Switcher and Manager umożliwia udawanie, że uzyskujesz dostęp do strony internetowej z innego systemu operacyjnego lub innej przeglądarki internetowej. Innymi słowy, możesz udawać, że przeglądasz witrynę za pomocą iPhone'a, podczas gdy w rzeczywistości uzyskujesz do niej dostęp z przeglądarki Mozilla Firefox. Możesz pobrać User-Agent Switcher and Manager dla przeglądarki Firefox stąd.\
Wappalyzer dostarcza informacji o technologiach używanych na odwiedzanych witrynach. Takie rozszerzenie jest przydatne, przede wszystkim gdy zbierasz wszystkie te informacje podczas przeglądania witryny jak każdy inny użytkownik. Zrzut ekranu Wappalyzera pokazano poniżej. Wappalyzer dla przeglądarki Firefox znajdziesz tutaj.

<br>

<br>

On Linux and macOS, the command to use is `traceroute 10.10.123.13`, and on MS Windows, it is `tracert 10.10.123.13`. `traceroute`&#x20;

\--- można sprawdzic adres routera w ostatnim hop-ie

<br>

<br>

\> telnet 10.10.123.13 PORT

<br>

GET / HTTP/1.1

host: telnet

HTTP/1.1 408 Request Timeout

Date: Fri, 06 Jun 2025 12:13:43 GMT

Server: Apache/2.4.61 (Debian)

Content-Length: 329

Connection: close

Content-Type: text/html; charset=iso-8859-1

<br>

<br>

<br>

NETCAT

\> nc 10.10.123.13 PORT

(port = 80)

<br>

<br>

<br>

| Command          | Example                                     |
| ---------------- | ------------------------------------------- |
| ping             | `ping -c 10 10.10.123.13` on Linux or macOS |
| ping             | `ping -n 10 10.10.123.13` on MS Windows     |
| traceroute       | `traceroute 10.10.123.13` on Linux or macOS |
| tracert          | `tracert 10.10.123.13` on MS Windows        |
| telnet           | `telnet 10.10.123.13 PORT_NUMBER`           |
| netcat as client | `nc 10.10.123.13 PORT_NUMBER`               |
| netcat as server | `nc -lvnp PORT_NUMBER`                      |

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>
