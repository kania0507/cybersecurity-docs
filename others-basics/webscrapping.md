# Webscrapping

_Web scraping_ to automatyczny proces pozyskiwania danych ze stron internetowych poprzez analizę ich struktury i ekstrakcję interesujących informacji.

<br>

#### **7 „dobrych” praktyk** _Web scraping_**u**

1\. Wykorzystuj API\
2\. Przestrzegaj zapisów z robots.txt (informuje robota internetowego, które obszary witryny\
nie powinny być przetwarzane ani skanowane, sprawdź ograniczenia np. DISALLOW / to blokada wszystkiego)\
3\. Przestrzegaj warunków korzystania z usługi (_Term of Service_)\
4\. Nie naruszaj [RODO](https://pl.wikipedia.org/wiki/Og%C3%B3lne_rozporz%C4%85dzenie_o_ochronie_danych) (dla UE) – uwaga na scrapowanie danych osobowych (imię, nazwisko, numer telefonu, adres, login, adres IP, informacje o numerze karty płatniczej, dane medyczne); „_legalnego powodu_” : uzasadniony interes, zgoda klienta\
5\. Nie szkodź stronie - nie powinno obciążać serwerów serwisu ani zakłócać normalnego działania strony; aby nie szkodzić próbować w nocy, ograniczyć ilość równoczesnych żądań do tej samej witryny z jednego IP;\
6\. Nie naruszaj praw autorskich - prawo do fizycznego dzieła takiego jak artykuł, zdjęcie, film, utwór, itp.\
Istnieją jednak wyjątki, w których można scrapować do woli, a następnie legalnie wykorzystywać dane bez naruszania praw autorskich, np.: na własny użytek publiczny, w celach dydaktycznych lub w celu prowadzenia działalności naukowej, w ramach prawa do cytatu.\
7\. Nie ukrywaj się – np. poprzez poprzez podanie w zmiennej USER\_AGENT swojego adresu mailowego w Scrapy.



NARZĘDZIA<br>

**Puppeteer** to biblioteka automatyzacji przeglądarki dla Node. js, która umożliwia sterowanie przeglądarką za pomocą prostego i nowoczesnego interfejsu JavaScript API. Najważniejszym zadaniem przeglądarki jest oczywiście przeglądanie stron internetowych.

To biblioteka JavaScript, która zapewnia interfejs API wysokiego poziomu do automatyzacji zarówno Chrome, jak i Firefox za pośrednictwem protokołu Chrome DevTools i WebDriver BiDi . Użyj go do automatyzacji wszystkiego w przeglądarce, od robienia zrzutów ekranu i generowania plików PDF po nawigację i testowanie złożonych interfejsów użytkownika oraz analizowanie wydajności.

Jest podobny do innych frameworków testujących przeglądarki, takich jak WebDriver. Tworzysz wystąpienie przeglądarki, otwierasz stronę internetową, a następnie manipulujesz stroną internetową za pomocą interfejsu API Puppeteer .

Puppeteer działa niezależnie od procesu przeglądarki, co umożliwia bezpieczną automatyzację potencjalnie złośliwych stron.

Przełączanie między trybami Headless i Headful : Aby zmniejszyć ryzyko wykrycia, przełączaj się między trybami Headless i Headful (z GUI). Dzięki temu Twoje działania związane ze scrapowaniem będą bardziej przypominać prawdziwe sesje przeglądania. Dostosowywanie agentów użytkownika: Witryny często wykrywają przeglądarki Headless, sprawdzając ciąg agenta użytkownika.

<br>

**Playwright** oferuje wszechstronność i zaawansowane funkcje, szczególnie cenne w większych projektach wymagających wsparcia wielu przeglądarek. Puppeteer natomiast excaluje w projektach skoncentrowanych na Chrome, oferując prostotę i wydajność. Oba narzędzia są aktywnie rozwijane i regularnie wzbogacane o nowe funkcje.

Playwright ma natywne testy aplikacji mobilnych, podczas gdy Puppeteer ma ograniczone wsparcie.

Playwright współpracuje z JavaScript, TypeScript, Python, .NET i Java; Puppeteer obsługuje wyłącznie JavaScript/TypeScript .

Playwright - Asynchroniczne i synchroniczne; puppeter – asynchroniczny;

laywright oferuje funkcje takie jak przechwytywanie zrzutów ekranu, generowanie plików PDF (tylko w trybie headless Chromium) i nagrywanie filmów na potrzeby sesji testowych. Umożliwia również monitorowanie i przechwytywanie żądań sieciowych, co jest przydatne do testowania interfejsów API, modyfikowania odpowiedzi na żądania i symulowania różnych warunków sieciowych.

Warto zwrócić uwagę na funkcję automatycznego oczekiwania w Playwright. Imituje ona (ludzkiego) użytkownika, czekając określoną ilość czasu po wypełnieniu formularza logowania i przed kliknięciem przycisku.

\
<br>

**Charles** Proxy (płatny), znany również jako Charles, to aplikacja proxy do debugowania sieci Web, używana przez programistów do przeglądania całego ruchu HTTP i SSL/HTTPS pomiędzy ich komputerem a Internetem .

Umożliwia użytkownikowi przeglądanie HTTP, HTTPS, HTTP / 2 i włącza ruch portów TCP dostępny z, do, lub przez komputer lokalny.

Programiści front-end używają Charlesa do debugowania żądań AJAX, analizowania wywołań REST API i rozwiązywania problemów z komunikacją przeglądarka-serwer . Możliwość modyfikowania żądań pomaga testować różne scenariusze bez zmiany kodu aplikacji.

\
<br>

<br>

**Burp** Suite to autorskie narzędzie programowe służące do oceny bezpieczeństwa i testów penetracyjnych aplikacji internetowych.

To zestaw narzędzi przeznaczonych do przeprowadzania testów bezpieczeństwa sieci. Podstawowa funkcjonalność obejmuje między innymi testowanie penetracyjne, analizę trafienia i włamań oraz systemy skanowania podatności, które automatycznie szukają zagrożeń.

<br>

<br>

<br>
