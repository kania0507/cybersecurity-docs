# AppSec - questions & answers

<mark style="background-color:blue;">Zadanie 1\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_</mark>

Wyobraź sobie, że tworzysz aplikację webową, która pozwala użytkownikom dodawać komentarze do artykułów. W ramach tej funkcji użytkownik może dołączyć do komentarza pliki (np. obrazy, PDF-y), które następnie będą wyświetlane (lub dostępne do pobrania) na stronie.

**Pytanie:**\
Jakie potencjalne zagrożenia bezpieczeństwa wiążą się z tą funkcjonalnością i jakie konkretne środki powinieneś zastosować, aby je zminimalizować? Uwzględnij zarówno część tekstową komentarza, jak i obsługę plików.

**Odpowiedź:**

**1. Cross-Site Scripting (XSS) w komentarzach**

* **Zagrożenie:** Użytkownik może próbować przesłać złośliwy kod JavaScript jako treść komentarza.
* **Zabezpieczenia:**
  * Escapowanie danych przed wyświetleniem w HTML.
  * Użycie tzw. „safe rendering” w frameworku (np. React domyślnie).
  * Nagłówki bezpieczeństwa: `Content-Security-Policy`, `X-XSS-Protection`.

***

**2. Złośliwe pliki (File Upload Vulnerabilities)**

* **Zagrożenie:** Przesłany plik może zawierać złośliwy kod (np. `.php`, `.js`, `.exe`) lub udawać bezpieczny (np. obrazek `.jpg` zawierający skrypt).
* **Zabezpieczenia:**
  * **Whitelist typów MIME**: akceptowanie tylko określonych typów (`image/png`, `image/jpeg`, `application/pdf`).
  * **Weryfikacja rozszerzenia i typu MIME** po stronie serwera.
  * **Skany antywirusowe** (np. przy użyciu ClamAV).
  * **Zmiana nazw plików i przechowywanie ich poza katalogiem publicznym** (np. w S3, CDN lub pod zmienioną ścieżką).
  * **Zablokowanie wykonywania przesłanych plików** (np. przez ustawienia serwera `X-Content-Type-Options: nosniff` i brak uprawnień `execute`).

***

**3. Ataki typu Content Sniffing i MIME Confusion**

* **Zagrożenie:** Przeglądarka może błędnie interpretować zawartość pliku i wykonać skrypt.
* **Zabezpieczenia:**
  * Wymuszenie nagłówka `Content-Disposition: attachment; filename="..."`.
  * Ustawienie `X-Content-Type-Options: nosniff`.

***

**4. Ograniczenie wielkości plików i rate limiting**

* **Zagrożenie:** Ataki DoS poprzez przesyłanie dużych plików lub wielu żądań.
* **Zabezpieczenia:**
  * Limit rozmiaru pliku (np. max 5 MB).
  * Rate limiting na endpointy uploadu.
  * Odrzucenie plików z dużą entropią lub nietypowym nagłówkiem binarnym.

***

**5. Przechowywanie i dostęp do plików**

* **Zagrożenie:** Bezpośredni dostęp do plików użytkowników bez autoryzacji.
*   **Zabezpieczenia:**

    * Generowanie tymczasowych URL-i (signed URLs).
    * Autoryzacja dostępu do pliku (np. tylko dla autora lub uprawnionych użytkowników).
    * Oddzielenie zasobów statycznych od aplikacji (CDN / osobny serwer).





#### <mark style="background-color:blue;">Zadanie2</mark> \_<mark style="background-color:blue;">\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_</mark>

#### Analiza luki w kodzie

**Opis:**

Poniższy fragment kodu pochodzi z kontrolera aplikacji w Node.js z użyciem Express. Użytkownik może przesłać komentarz i opcjonalnie dodać plik (np. obrazek). Plik jest przechowywany na serwerze i dostępny przez URL.

```javascript
javascriptKopiujEdytujconst express = require('express');
const multer = require('multer');
const fs = require('fs');
const path = require('path');

const app = express();
const upload = multer({ dest: 'uploads/' });

app.post('/submit-comment', upload.single('file'), (req, res) => {
    const comment = req.body.comment;
    const file = req.file;

    // Zapisz komentarz i plik
    fs.writeFileSync(`comments/${Date.now()}.txt`, comment);

    let fileUrl = '';
    if (file) {
        const targetPath = path.join(__dirname, 'public', 'uploads', file.originalname);
        fs.renameSync(file.path, targetPath);
        fileUrl = `/uploads/${file.originalname}`;
    }

    res.send(`Komentarz zapisany. <a href="${fileUrl}">Zobacz plik</a>`);
});
```

***

#### ❓ Pytanie do kandydata:

Zidentyfikuj potencjalne luki bezpieczeństwa w tym kodzie oraz zaproponuj konkretne poprawki.

***

#### ✅ Przykładowe odpowiedzi (czego szukamy):

**1. Brak walidacji i filtrowania typu pliku**

* **Luka:** Pliki o niebezpiecznych rozszerzeniach (np. `.php`, `.html`) mogą zostać przesłane i wykonane na serwerze.
* **Poprawka:** Dodaj whitelistę rozszerzeń i MIME-typów. Zmień nazwę pliku (nie używaj `originalname`) i przechowuj go w katalogu niedostępnym z zewnątrz.

**2. Możliwość XSS przez `fileUrl`**

* **Luka:** Użytkownik może przesłać plik o nazwie zawierającej kod HTML lub JS, np. `<script>alert(1)</script>.png`.
* **Poprawka:** Nigdy nie używaj `file.originalname` do tworzenia nazw lub URL-i bez sanityzacji. Zastąp UUID-em lub `Date.now()`.

**3. Path Traversal**

* **Luka:** Brak walidacji `file.originalname` pozwala na ataki typu path traversal, np. `../../malicious.js`.
* **Poprawka:** Użyj `path.basename()` lub generuj nazwę samodzielnie.

**4. Zapis komentarza bez walidacji**

* **Luka:** Komentarz zapisywany jako plik tekstowy bez oczyszczenia — może zawierać kod HTML/JS i zostać wyświetlony w niebezpieczny sposób.
* **Poprawka:** Sanityzuj dane wejściowe przed zapisaniem i wyświetlaniem.

**5. Brak ochrony przed DoS i spamem**

* **Luka:** Brak limitu wielkości pliku i częstotliwości żądań.
* **Poprawka:** Ogranicz rozmiar pliku, wprowadź throttling lub captcha.





_w trakcie.._
