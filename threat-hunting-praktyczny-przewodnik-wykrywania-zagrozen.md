# Threat Hunting – praktyczny przewodnik wykrywania zagrożeń



Threat hunting to proces **proaktywnego poszukiwania zagrożeń**, które mogły ominąć klasyczne mechanizmy detekcji. Zamiast reagować na alerty, analityk zakłada możliwość kompromitacji i aktywnie jej szuka.

Podejście to jest zgodne z praktykami opisywanymi przez:

• **MITRE**\
• **CISA**\
• **Microsoft**\
• **Trend Micro**

Źródła na końcu.

### 1. Przygotowanie i planowanie

#### 1.1 Zrozum swoją infrastrukturę

**Co robić:**\
Zidentyfikuj elementy o najwyższym ryzyku i wartości operacyjnej.

**Typowe obszary krytyczne:**

• Active Directory / Entra ID\
• Systemy finansowe i bazy danych\
• VPN / dostęp zdalny\
• Usługi chmurowe / IAM

**Przykłady:**

• Finanse – serwery z danymi klientów\
• Infrastruktura IT – kontrolery domeny\
• Chmura – systemy tożsamości (SSO / IAM)

**Dlaczego:**\
Threat hunting jest procesem kontekstowym. Anomalia na serwerze testowym ≠ anomalia na kontrolerze domeny.

Źródło:\
[https://www.trendmicro.com/pl\_pl/what-is/threat-detection/threat-hunting.html](https://www.trendmicro.com/pl_pl/what-is/threat-detection/threat-hunting.html)

#### 1.2 Włącz logowanie i widoczność

**Co robić:**\
Zapewnij pełną telemetrykę z kluczowych warstw.

**Minimalny zestaw danych:**

• Endpointy (EDR / XDR)\
• Sieć (firewall, proxy, DNS, VPN)\
• Tożsamość (AD / Entra / IAM)

**Przykłady istotnych logów:**

• PowerShell / linie poleceń\
• Logowania RDP / VPN\
• Zmiany uprawnień / grup AD\
• Połączenia sieciowe

**Dlaczego:**\
Threat hunting bez danych to zgadywanie.

Źródło:\
[https://www.trendmicro.com/pl\_pl/what-is/threat-detection/threat-hunting.html](https://www.trendmicro.com/pl_pl/what-is/threat-detection/threat-hunting.html)

#### 1.3 Zbuduj baseline (normalny profil)

**Co robić:**\
Zdefiniuj, jak wygląda normalne zachowanie środowiska.

**Obszary do obserwacji:**

• Godziny logowań\
• Typowe procesy administracyjne\
• Regularny ruch sieciowy\
• Standardowe lokalizacje użytkowników

**Przykłady baseline:**

• Pracownicy logują się 7:00–18:00\
• PowerShell uruchamiany głównie przez IT\
• Serwer aplikacyjny nie wykonuje ruchu DNS\
• VPN używany z ograniczonej liczby krajów

**Dlaczego:**\
Threat hunting = analiza odchyleń od normy.

Źródło:\
[https://www.cycognito.com/learn/threat-hunting/](https://www.cycognito.com/learn/threat-hunting/)

### 2. Formułowanie hipotez (kluczowy krok)

#### 2.1 Zbuduj hipotezę

**Co robić:**\
Formułuj testowalne pytania.

**Struktura dobrej hipotezy:**

• Zakres czasowy\
• Kontekst (system / użytkownicy)\
• Obserwowalne wskaźniki

**Przykłady:**

• „Czy w ostatnich 72 godzinach wystąpiły oznaki credential dumpingu?”\
• „Czy konta uprzywilejowane logowały się z nietypowych lokalizacji?”\
• „Czy procesy spoza whitelisty wykonywały nietypowe połączenia sieciowe?”

**Dlaczego:**\
Hunting bez hipotezy prowadzi do chaotycznej analizy logów.

Źródło:\
https://www.cisa.gov/resources-tools/resources/threat-hunting

### 3. Mapowanie zagrożeń i narzędzia

#### 3.1 Użyj MITRE ATT\&CK jako ramy

Framework **MITRE ATT\&CK** opisuje techniki atakujących.

**Co robić:**

1. Wybierz techniki odpowiadające hipotezie
2. Powiąż je z danymi telemetrycznymi

**Przykłady technik:**

• T1059 – Command Execution (PowerShell)\
• T1021 – Remote Services (lateral movement)\
• T1003 – Credential Dumping

**Jak mapowanie pomaga:**

• Zamienia intuicję w strukturę analityczną\
• Ułatwia budowę zapytań\
• Standaryzuje detekcję

**Gdzie realizować:**

• **Microsoft Sentinel** / SIEM\
• EDR / XDR\
• Analiza ręczna (analityk)

Źródła:\
[https://attack.mitre.org](https://attack.mitre.org)\
[https://learn.microsoft.com/en-us/azure/sentinel/](https://learn.microsoft.com/en-us/azure/sentinel/)

### 4. Analiza danych – wykrywanie i wyszukiwanie

#### 4.1 Zapytania w SIEM / EDR

**Co robić:**\
Filtruj dane pod kątem anomalii i wzorców.

**Przykłady zapytań logicznych:**

• Nietypowe logowania\
• Rzadkie procesy\
• Nienaturalny ruch sieciowy

**Przykłady praktyczne:**

• „Procesy PowerShell spoza standardowych katalogów”\
• „Logowania RDP poza baseline”\
• „Połączenia na rzadko używane porty”

**Dlaczego:**\
SIEM umożliwia analizę dużych wolumenów danych.

Źródło:\
[https://learn.microsoft.com/en-us/azure/sentinel/hunting](https://learn.microsoft.com/en-us/azure/sentinel/hunting)

#### 4.2 Korelacja i wzorce

**Co robić:**\
Łącz dane z różnych źródeł.

**Przykłady korelacji:**

• Logowanie + zmiana uprawnień\
• Proces + połączenie sieciowe\
• DLL injection + ruch C2

**Dlaczego:**\
Ataki to sekwencje zdarzeń, nie pojedyncze logi.

Źródło:\
https://www.cisa.gov/resources-tools/resources/threat-hunting

### 5. Ocena i dokumentacja

#### 5.1 Notuj wyniki i wnioski

**Co robić:**\
Dokumentuj każdą hipotezę.

**Przykłady wyników:**

• Brak anomalii → luka w telemetryce\
• Wykryta anomalia → nowa detekcja\
• Potwierdzone zagrożenie → eskalacja IR

**Dlaczego:**\
Threat hunting buduje wiedzę organizacyjną.

#### 5.2 Automatyzuj i twórz playbooki

**Co robić:**\
Automatyzuj powtarzalne scenariusze.

**Przykłady:**

• Reguły SIEM na znane techniki\
• Automatyczne wzbogacanie TI\
• Playbooki reakcji

**Dlaczego:**\
Zmniejsza obciążenie SOC.

Źródło:\
https://learn.microsoft.com/en-us/azure/sentinel/automation

### 6. Praktyczne przykłady sytuacji

#### 6.1 Hipoteza: podejrzane logowania

**Działanie:**

• Logowania poza baseline\
• Nietypowe lokalizacje\
• Nierealistyczne „impossible travel”

**Co sprawdzić:**

• ASN / reputacja IP\
• MFA / mechanizmy obejścia\
• Historia aktywności konta

#### 6.2 Hipoteza: lateral movement

**Działanie:**

• Remote Services / RDP / WinRM\
• Nietypowe relacje host–host

**Mapowanie:**

• Technika T1021

**Co analizować:**

• Procesy inicjujące sesje zdalne\
• Ruch SMB / RPC\
• Nietypowe konta

#### 6.3 Hipoteza: eskalacja uprawnień

**Działanie:**

• Zmiany grup AD\
• Nietypowe delegacje

**Mapowanie:**

• Privilege Escalation

## Co w logach Microsoft powinno zaniepokoić

Bazując na praktykach SOC / Microsoft:

• Impossible Travel\
• Nietypowe OAuth Consent Grants\
• Tworzenie reguł przekierowania poczty\
• Seria nieudanych MFA (MFA fatigue)\
• Logowania z anonimowych sieci / TOR\
• Nietypowe użycie PowerShell\
• Dostęp do LSASS / credential dumping

Źródło:\
[https://learn.microsoft.com/en-us/security/](https://learn.microsoft.com/en-us/security/)

## Co w mailach powinno zaniepokoić

Wzorce obserwowane w phishing / BEC:

• Display Name Spoofing\
• Domeny podobne (lookalike domains)\
• Nietypowe linki OAuth / logowania\
• QR phishing\
• Nietypowe typy załączników\
• Nacisk na pilność / strach / presję

Źródło:\
[https://www.cisa.gov/news-events/news/avoiding-social-engineering-and-phishing-attacks](https://www.cisa.gov/news-events/news/avoiding-social-engineering-and-phishing-attacks)

## Jak zrobić mapowanie technik praktycznie

1. Wybierz technikę w MITRE ATT\&CK
2. Powiąż ją z hipotezą
3. Sprawdź dostępność danych
4. Zbuduj zapytanie / regułę
5. Oceń wyniki

**SIEM vs analiza ręczna**

SIEM → skala, automatyzacja\
Ręcznie → kontekst, niestandardowe przypadki

Najlepsze efekty daje połączenie obu.

## Sprawdzone źródła

MITRE ATT\&CK\
[https://attack.mitre.org](https://attack.mitre.org)

CISA – Threat Hunting\
https://www.cisa.gov/resources-tools/resources/threat-hunting

Microsoft Sentinel – Hunting\
[https://learn.microsoft.com/en-us/azure/sentinel/hunting](https://learn.microsoft.com/en-us/azure/sentinel/hunting)

Trend Micro – Threat Hunting\
[https://www.trendmicro.com/pl\_pl/what-is/threat-detection/threat-hunting.html](https://www.trendmicro.com/pl_pl/what-is/threat-detection/threat-hunting.html?utm_source=chatgpt.com)

CISA – Phishing\
[https://www.cisa.gov/news-events/news/avoiding-social-engineering-and-phishing-attacks](https://www.cisa.gov/news-events/news/avoiding-social-engineering-and-phishing-attacks)

***

J
