# Nagłówki bezpieczeństwa, mechanizmy przeglądarkowe

## 1) CSP — Content Security Policy

**Co to jest:** nagłówek (albo `<meta http-equiv="Content-Security-Policy" ...>`) określający skąd przeglądarka może ładować zasoby (skrypty, style, obrazy, ramki, itp.). Ma zapobiegać XSS i ładowaniu złośliwych zasobów.

**Kluczowe dyrektywy:**

* `default-src` — domyślne źródła.
* `script-src`, `style-src`, `img-src`, `connect-src`, `frame-ancestors` itd.
* `object-src 'none'` — blokuje plug-iny (zalecane).
* `report-uri` / `report-to` — raportowanie naruszeń CSP.

**Poprawna, bezpieczna konfiguracja (zasady):**

* Stosuj zasadę _najmniejszego zaufania_ — zezwalaj tylko na konkretne źródła domen i protokoły.
* Unikaj `'unsafe-inline'` i `'unsafe-eval'` w `script-src` i `style-src`.
* Używaj nonce (`'nonce-<random>'`) lub hashów (`'sha256-...'`) dla dynamicznie wstawianych skryptów zamiast `'unsafe-inline'`.
* Oddziel polityki dla produkcji i środowisk testowych.
* Włącz tryb reporterski (`Content-Security-Policy-Report-Only`) na początku, żeby zbierać błędy bez wymuszania (monitorowanie).
* Ustal `frame-ancestors 'self'` zamiast X-Frame-Options, jeżeli potrzebujesz większej kontroli.

**Typowe błędy i jak prowadzą do obejścia CSP (opis, bez payloadów):**

* Zezwolenie na `'unsafe-inline'` → praktycznie unieważnia ochronę przed XSS opartą na CSP.
* Zezwolenie na szerokie wildcardy (`*.example.com` albo `https:`) → dopuszcza ładowanie z wielu zewnętrznych źródeł, w tym potencjalnie kompromitowanych CDN.
* Używanie starego `report-only` bez przejścia do wymuszania → aplikacja pozornie jest zabezpieczona, ale w praktyce nie blokuje ataków.
* Pozwolenie `data:` lub `blob:` w `script-src` → umożliwia załadowanie kodu bezpośrednio w formie danych (łatwiej obejść ograniczenia).
* Dynamiczne generowanie nonce bez odpowiedniej entropii lub ponowne używanie tego samego nonce wielokrotnie → osłabia bezpieczeństwo.

**Jak wykryć i ocenić CSP (narzędzia):**

* Przeglądarka DevTools (Console → błędy CSP).
* Mozilla Observatory / Security Headers (securityheaders.com) — ocena nagłówków.
* Google CSP Evaluator — statyczna analiza polityki CSP, wykrywa słabe miejsca.
* report-uri / Report-To — zbieranie realnych naruszeń w produkcji.
* CSP Mitigator / csp-wizard — pomoc przy komponowaniu bezpiecznej polityki.

***

## 2) Access-Control-Allow-Origin / Credentials (CORS)

**Co to jest:** mechanizm kontroli dostępu dla zapytań z originów (przeglądarka bada politykę CORS). Główne nagłówki: `Access-Control-Allow-Origin`, `Access-Control-Allow-Credentials`, `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`.

**Typowe błędy i ich konsekwencje:**

* `Access-Control-Allow-Origin: *` **+** `Access-Control-Allow-Credentials: true` — niezgodne: przeglądarki zablokują to (ale serwery czasem zwracają niebezpieczne kombinacje lub reflektują origin niewłaściwie). Jeśli serwer odpowiada na żądanie pochodzące z dowolnego originu i jednocześnie akceptuje ciasteczka/autoryzację, to może dojść do wycieku autoryzacji do niezamierzonych originów.
* Dynamiczne _odbijanie_ (echo) nagłówka Origin bez walidacji przeciwko białej liście → atakujący może wysłać żądanie z dowolnego originu i uzyskać dostęp do zasobów chronionych poświadczeniami ofiary (jeśli przeglądarka dołącza cookie).
* Brak obsługi preflightów lub błędna lista metod/headers → może powodować nieoczekiwane odrzucenia lub nadmiarowe uprawnienia.

**Dobre praktyki (konfiguracja):**

* Nie używaj wildcard (`*`) jeżeli `Allow-Credentials: true`.
* Implementuj whitelistę originów po stronie serwera i **odprawdzaj** `Origin` przed zwróceniem `Access-Control-Allow-Origin`.
* Zwracaj `Access-Control-Allow-Credentials: true` tylko jeśli naprawdę potrzebujesz wysyłać cookies/credentials cross-origin i tylko dla zaufanych originów.
* Minimalizuj `Access-Control-Allow-Headers`/`Methods` do tego, co jest niezbędne.
* Zabezpiecz endpointy autoryzacyjne dodatkowymi mechanizmami (CSRF tokeny, SameSite cookie).

***

## 3) Pozostałe nagłówki bezpieczeństwa — krótko i praktycznie

| Nagłówek                                                       | Co robi                                                              | Rekomendowana konfiguracja / uwagi                                                                                                                                        |
| -------------------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Strict-Transport-Security` (HSTS)                             | Nakazuje przeglądarce łączyć się tylko przez HTTPS przez zadany czas | `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload` — włącz po upewnieniu się, że HTTPS działa wszędzie. `preload` wymaga zgłoszenia do listy HSTS. |
| `X-Frame-Options` / `Content-Security-Policy: frame-ancestors` | Zapobiega clickjackingu (ładowaniu w ramkach)                        | Stosuj `DENY` lub `SAMEORIGIN`, lub lepiej `Content-Security-Policy: frame-ancestors 'self' https://trusted.example`                                                      |
| `Referrer-Policy`                                              | Kontroluje jakie informacje referera są wysyłane                     | Preferowane: `no-referrer-when-downgrade`, `strict-origin-when-cross-origin` lub `no-referrer` zależnie od potrzeby ochrony prywatności.                                  |
| `X-Content-Type-Options: nosniff`                              | Zapobiega „sniffowaniu” typu MIME                                    | Ustaw zawsze — pomaga zapobiegać uruchomieniu złośliwych plików.                                                                                                          |
| `Permissions-Policy` (dawniej Feature-Policy)                  | Kontroluje dostęp do API przeglądarki (geolokacja, kamera itd.)      | Wyłączaj funkcje które nie są używane: `Permissions-Policy: geolocation=(), camera=()`                                                                                    |
| `Content-Security-Policy`                                      | (omówione wyżej)                                                     | Używaj go jako centralnego punktu kontroli zasobów.                                                                                                                       |

***

## 4) Supply chain attacks — import skryptów z zewnętrznych serwisów

**Co to jest:** atak polegający na wykorzystaniu zaufanego łańcucha dostaw — np. kompromitacja CDN, pakietu npm, zależności JS — by dostarczyć złośliwy kod do końcowych użytkowników.

**Przykłady wektorów (opisowo):**

* Kompromitacja CDN (np. ktoś wgra złośliwy plik do CDN lub przejmie konto).
* Złośliwy lub przejęty pakiet w repozytorium publicznym (npm, PyPI).
* Typosquatting — podstawienie biblioteki o podobnej nazwie.
* Zewnętrzne skrypty ładowane przez stronę (third-party ads, analytics).

**Skuteczny przykład zagrożenia (bez instrukcji):**

* Strona ładuje globalny skrypt analityczny z CDN bez SRI i bez ograniczeń CSP. Jeśli CDN zostanie kompromitowany, złośliwy kod wykona się w kontekście strony i może kraść ciasteczka, wypaść dane formularzy, wykonywać transakcje itp.

**Mitigacje:**

* **Subresource Integrity (SRI)**: dodaj atrybut `integrity` do `<script>`/`<link>` dla zasobów z CDN — przeglądarka sprawdzi hash pliku przed wykonaniem. (Uwaga: SRI nie działa dla zasobów dynamicznie modyfikowanych lub jeśli używasz CSP z `nonce` zamiast zewnętrznych skryptów.)
* **CSP**: zablokuj ładowanie skryptów z niesprawdzonych domen, używaj `script-src` z whitelistą.
* **Lockfile / Pinowanie wersji** w menedżerach pakietów + skanowanie zależności (Snyk, Dependabot, npm audit).
* **Minimalizuj wczytywanie zewnętrznych skryptów**: hostuj ważne biblioteki lokalnie, użyj prywatnych registrów.
* **Code review i skanowanie** zależności przed wdrożeniem.
* **Content Security Policy + Nonce/Hash**: nawet gdy skrypt pochodzi z zaufanej domeny, CSP z hash/nonce ogranicza wykonanie nieautoryzowanego kodu.

***

## 5) Przykłady wykorzystania błędów + jak je zmitigować (scenariusze)

1. **Brak X-Frame-Options / frame-ancestors**
   * _Wykorzystanie:_ clickjacking (atakujący ładuje stronę w ukrytej ramce i nakłada elementy tak, by użytkownik wykonał akcję).
   * _Mitigacja:_ `X-Frame-Options: DENY` lub `Content-Security-Policy: frame-ancestors 'self'`.
2. **CSP zawierające `'unsafe-inline'`**
   * _Wykorzystanie:_ atakujący może wstrzyknąć skrypt inline (XSS) i on zostanie wykonany.
   * _Mitigacja:_ usuń `'unsafe-inline'`; stosuj nonce/hashi; waliduj wejścia po stronie serwera.
3. **CORS: `Access-Control-Allow-Origin: *` + wrażliwe API**
   * _Wykorzystanie:_ jeśli serwer nie wymaga credentials i zwraca dane publiczne, wildcard jest OK; tam gdzie używane są ciasteczka/autoryzacja, wildcard umożliwia wyciek (gdy serwer nie sprawdza origin).
   * _Mitigacja:_ użyj whitelisty originów, weryfikuj `Origin` po stronie serwera, nie pozwalaj wildcard przy `Allow-Credentials: true`.
4. **Brak HSTS**
   * _Wykorzystanie:_ man-in-the-middle może wymusić downgrade na HTTP i przejąć sesję.
   * _Mitigacja:_ `Strict-Transport-Security: max-age=...; includeSubDomains; preload` + przekierowanie HTTP→HTTPS.
5. **Ładowanie skryptów z CDN bez SRI i bez ograniczeń CSP**
   * _Wykorzystanie:_ kompromitacja CDN powoduje wykonanie złośliwego JS.
   * _Mitigacja:_ SRI, CSP, pinowanie wersji, lokalne hostowanie krytycznych bibliotek.

***

## 6) Lista praktycznych kroków / checklist (szybko do wdrożenia)

* Wdróż **CSP** w trybie `report-only`, zbieraj raporty, popraw i przełącz na enforce.
* Usuń `'unsafe-inline'` i `'unsafe-eval'` z CSP; używaj nonce/hashes.
* Weryfikuj i whitelistuj `Origin` dla CORS; nie używaj `*` przy cookie/credentials.
* Ustaw `Strict-Transport-Security` z `includeSubDomains` i przygotuj się do `preload`.
* Ustaw `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY` lub CSP `frame-ancestors`, `Referrer-Policy`.
* Wprowadź **SRI** dla zewnętrznych skryptów i ogranicz liczbę third-party skryptów.
* Skonfiguruj automatyczne skanery zależności + audyty bezpieczeństwa (Dependabot, Snyk).
* Monitoruj raporty CSP (`report-uri`) i logi serwera.
* Edukuj zespół: nie zatwierdzaj `'unsafe-*'`, przeglądaj zależności.

***

## 7) Narzędzia przydatne w ocenie i testowaniu (audyt, nie atak)

* **Przeglądarkowe DevTools** — konsola CSP, network, security.
* **Mozilla Observatory**, **SecurityHeaders.com** — ocena nagłówków i sugestie.
* **Google CSP Evaluator** — analiza polityk CSP.
* **report-uri.com / Report-To** — zbieranie raportów CSP.
* **Snyk, Dependabot, npm audit** — skanowanie zależności (supply chain).
* **Subresource Integrity (SRI) kalkulatory** — generowanie hashy dla SRI.
* **Burp Suite / ZAP** — do audytu bezpieczeństwa (używaj odpowiedzialnie, na środowiskach testowych lub za zgodą).
* **CI/CD checks** — skrypty testujące obecność i poprawność nagłówków w buildzie.

***

## 8) Krótkie przykładowe nagłówki (bez opisu wykorzystywania)

Bezpieczna podstawowa konfiguracja nagłówków (przykład do użycia jako inspiracja):

```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted.cdn.com 'nonce-...'; object-src 'none'; frame-ancestors 'self'; base-uri 'self'; report-uri https://report.example.com/csp
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), camera=()
Access-Control-Allow-Origin: https://trusted-client.example.com
Access-Control-Allow-Credentials: true
```

(Uwaga: nonce powinien być losowy i generowany per-request; zamiast wildcardów stosuj konkretne domeny).
