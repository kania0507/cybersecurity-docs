# Etyczny hacking

Etyczny hacking – wykorzystanie wiedzy z zakresu cyberbezpieczeństwa w celu zidentyfikowania i rozwiązania potencjalnych luk w systemach komputerowych, sieciach, aplikacjach w legalny sposób (za zgodą). Celem jest lepsze zabezpieczenie systemu przed atakami.

<br>

Testy penetracyjne (pentesty) – kontrolowane próby złamania zabezpieczeń w systemach, sieciach lub aplikacjach. Ocena poziomu bezpieczeństwa oraz identyfikacja możliwych zagrożeń (luk bezp).

Etapy:

\- PRZYGOTOWANIE: ustalenie zakresu testu, określenie celów, identyfikacja zasobów, sporządzenie harmonogramu, uzyskanie zgody od właściciela systemu

\- ZBIERANIE INFORMACJI: OSINT,

\- ANALIZA ZAGROŻEŃ, środowisko testowe a la rzeczywiste (serwery/maszyny wirtualne),

skanowanie i identyfikacja słabości

\- ATAKI (exploitation): SQL, XSS, hasła itp.

uzyskanie dostępu

\- RAPORT zawierający słabości, opis ryzyka, rekomendacje, ocena ryzyka





**ŚRODOWISKA PRACY**

LINUX TSURUGI (Ubuntu) – zawiera programy do odzyskiwania danych, analizy plików (na NTFS, FAT), badania rejestrów, OSINT, narzędzia do ekstrakcji i analizy metadanych plików;

narzędzie do tworzenia raportów; bezpieczne i prywatne;<br>

PARROT OS – lekki; edycje: securitu, home, cloud; wiele narzędzi do testów penetracyjnych, analizy sieci, łamanie haseł itp.

narzędzia do zachowania prywatności i anonimowości w sieci;<br>

KALI LINUX (debian) – do testowania zabezpieczeń SO, aplikacji, sieci w sposób legalny;

ponad 600 narzędzi, dedykowane jądro systemu, rozbudowana dokumentacja i społeczność, aktualizacje;



Oprogramowanie wirtualizacyjne typu opensource:

\- Vmware

\- Oracle VirtualBox

\- Microsoft Hyper-v<br>

Podstawowe komendy linuxa:

\> sudo apt update<br>

\> touch plik.txt

\> cat > plik2.txt

<br>

\> nano plik.txt

<br>

\> cat plik.txt plik2.txt > all.txt<br>

\> rm

\> rmdir<br>

\> passwd<br>

\> ifconfig



Sumy kontrolne:

\> md5sum nowy.txt

\> sha1sum nowy.txt



\> ls -l

\> chmod 777 nowy.txt

\> chmod o-x nowy.txt (usuwanie uprawnien)<br>

**PODSTAWY SIECI KOMPUTEROWYCH**

sieć komputerowa – zbiór połączonych ze sobą komputerów lub innych urządzeń, które mogą komunikować się ze sobą i wymieniać informacje.

LAN – lokalna sieć w obrębie budynku;

MAN – sieci miejskie, np. w różnych miastach ta sama organizacja;

WAN – sieci szerokopasmowe, duże obszary geograficzne;

PAN – sieci osobiste (telefon + laptop)

<br>

**TOPOLOGIE**: topologia gwiazdy (urządzenia podłączone do jednego huba), magistrali (po kablu, awaria zakłóca całą sieć), pierścienia (urządzenie połączone z 2 sąsiednimi urządzeniami), zamknięta, jednokierunkowa (awaria = przerwanie komunikacji);

siatkowa (połączenie każde z każdym, niezawodna, kosztowna, skomplikowana w większych sieciach); hubrydowa; drzewa (gwiazda + magistrala; większe sieci – hierarchiczne struktury);

<br>

**TCP/IP** – model protokołów, sieciowy, praktyczny, 4 warstwy:

aplikacji np. API, kodowanie i formatowanie, zabezpieczanie, szyfrowanie, autoryzacja, apl. Klienckie i serwerowe) – protokoły: HTTP (przegladarka a serwer), HTTPS, FTP, SMTP (przesyłanie e-mail między serwerami pocztowymi), POP3 (pobieranie e-mail z serwera), DNS (przetwarza adresy URL na IP),

transportu – zarządzanie przesyłaniem danych, segmentacja i reasemblacja danych, adresacja portów, nadzoruje szybkość przesyłania danych, kontrola błędów – protokoły: TCP (przesyłanie danych między aplikacjami na różnych urządzeniach w sieci, w odpowiedniej kolejności, np. przeglądarkach, poczcie); UDP (jest szybszy, ale nie gwarantuje niezawodnej komunikacji, bez sprawdzenia poprawności i możliwości retransmisji np. w grach online, strumieniowanie wideo);

internetowa – routowanie danych, zarządzanie trasą, przetwarza adresy IP, by dane dotarły z punktu A do B, do celu, najbardziej efektywnie; Przesyłane są pakiety – protokoły: IPv4 (32bitowy adres), IPv6, ICMP (informacje o stanie sieci i komunikowania się z routerami, komunikaty o błędach), RIP (Routing Information Protocol – do obliczania najlepszych tras);

dostępu do sieci – przekazuje dane przez fizyczne połączenia między urządzeniami (karty sieciowe lub modemy), przypisuje adresy MAC do otrzymanych pakietów (ramki), adresy MAC indentyfikują urządzenia w sieci; warstwa kontroluje sposób w jaki dane są przekazywane przez fizyczne media transmisyjne jak światłowody, fale radiowe – protokoły: Ethernet;

<br>

<br>

**ISO/OSI** – model abstrakcyjny, opisujący architekturę sieci komputerowych, służy do projektowania sieci; 7warstw:

aplikacji – interakcja użytkownika, usługi: strony www, poczta, komunikatory; komunikacja między różnymi aplikacjami w różnych sieciach;

prezentacji – przetwarzanie i formatowanie danych dla aplikacji; kodowanie, kompresja, szyfrowanie, konwersja na różne formaty;

sesji – zarządzanie sesjami między aplikacjami; kontrola dostępu i autoryzacja;

transportu – kontrola przepływu danych (TCP/UDP);

sieci (internetowa) – adresacja logiczna i zarządzanie trasowaniem, wybór najlepszej trasy;

łącza danych – kontrola błędów, zarządzaniem dostępem do medium transmisyjnego oraz kontrola przepływu danych;

fizyczna – fizyczne połączenie i transmisja danych przez medium transmisyjne (przewody, światłowody, fale radiowe (napięcia elektryczne,poziomy sygnałów, częstotliwość, metody kodowania), topologie;



**Najczęstsze ataki w zależności od warstwy:**

\- aplikacji – phishing i email, łamanie haseł, przepełnienie bufora, SQL injection

\- prezentacji – wstrzykiwanie kodu, dołączanie plików, phishing

\- sesji – przejęcie sesji, malware, XSS

\- transportowa – skanowanie portów, DDoS

\- sieciowa – man in the middle

\- łącza danych - spoofing

\- fizyczna - sniffing

<br>

<br>

<br>
