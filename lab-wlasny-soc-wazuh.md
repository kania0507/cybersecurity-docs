# LAB: własny SOC, Wazuh

Oto konspekt i materiały pomocnicze do modułu szkoleniowego:\
&#xNAN;**„SIEM – Analiza logów i alertów”**

***

### 🔹 1. Wprowadzenie do funkcji SIEM i jego architektury

#### Co to jest SIEM (Security Information and Event Management)?

SIEM to system służący do:

* **Zbierania** logów z różnych źródeł (systemy operacyjne, aplikacje, urządzenia sieciowe),
* **Analizy i korelacji** zdarzeń w czasie rzeczywistym,
* **Generowania alertów** na podstawie zdefiniowanych reguł,
* **Przechowywania danych** na potrzeby dochodzeń i zgodności z przepisami (compliance).

#### Kluczowe komponenty SIEM:

* **Collector/Agent** – zbiera logi z różnych systemów,
* **Parser** – przetwarza dane do ujednoliconego formatu,
* **Correlation Engine** – analizuje zdarzenia pod kątem zależności i anomalii,
* **Dashboard/Interface** – prezentuje dane analitykowi SOC,
* **Storage/Archive** – przechowuje logi i zdarzenia historyczne.

#### Przykładowe systemy SIEM:

* Splunk, IBM QRadar, ArcSight, ELK Stack (Elastic), Wazuh, Microsoft Sentinel.

***

### 🔹 2. Rola SIEM w SOC L1

#### Zadania analityka SOC L1:

* Monitorowanie alertów z SIEM w czasie rzeczywistym,
* Wstępna analiza zdarzeń – identyfikacja false positives,
* Eskalacja poważniejszych incydentów do SOC L2/L3,
* Tworzenie krótkich raportów z incydentów,
* Śledzenie aktywności użytkowników i systemów.

#### Użycie SIEM:

* L1 pracuje głównie na dashboardzie SIEM, korzystając z:
  * alertów korelacyjnych,
  * reguł detekcji (np. brute-force, malware execution),
  * zapytań do logów (np. za pomocą języka KQL – w Sentinel, SPL – w Splunk).

***

### 🔹 3. Źródła logów: Windows Event Logs, Sysmon, firewall

#### Windows Event Logs:

* **Security** – logi dotyczące logowań, tworzenia użytkowników, zmian uprawnień.
* **System** – uruchamianie/usługi/drivery.
* **Application** – błędy aplikacji, np. AV, Office.

#### Sysmon (System Monitor):

* Microsoftowy narzędzie do zaawansowanego monitoringu procesów.
* Generuje logi typu:
  * uruchomienie procesu (Event ID 1),
  * ładowanie bibliotek DLL (ID 7),
  * połączenia sieciowe (ID 3),
  * modyfikacje rejestru (ID 13, 14).

#### Firewalle i urządzenia sieciowe:

* Dostarczają logi o:
  * otwieranych portach,
  * połączeniach przychodzących/wychodzących,
  * próbach skanowania lub ataków DoS.

***

### 🔹 4. Ćwiczenia: analiza i korelacja zdarzeń z logów na przykładzie ataków

#### Przykład 1: Wykrycie ataku brute-force na RDP

**Logi z Windows Security:**

* Event ID 4625 (failed logon) z licznymi próbami z różnych IP,
* Korelacja: wiele prób w krótkim czasie na tego samego użytkownika.

**Reguła korelacyjna SIEM:**

```
Jeśli >10 logowań nieudanych (4625) z tego samego IP w ciągu 5 minut → Alert
```

***

#### Przykład 2: Wykrycie malware przez Sysmon

**Logi z Sysmon:**

* ID 1: Podejrzany proces uruchomiony z folderu tymczasowego,
* ID 3: Połączenie do domeny C2 (Command & Control),
* ID 11: Zmiana pliku systemowego.

**Analiza korelacyjna:**

* Uruchomienie pliku `.exe` z `AppData\Temp`,
* Szybkie połączenie do nieznanej domeny IP,
* Modyfikacje w rejestrze lub plikach systemowych.

***

#### Przykład 3: Analiza działania firewalla

* Logi z zapory: odrzucone połączenia z IP spoza kraju,
* Korelacja z próbami logowania (Windows 4625 + firewall deny),
* Możliwa próba ataku z zewnątrz.

***

### Propozycja ćwiczenia praktycznego

**Scenariusz:**

* Udostępnione logi Sysmon + Security + firewall (np. w pliku CSV).
* Zadanie:
  1. Znaleźć próbę ataku brute-force,
  2. Wykryć podejrzane uruchomienia procesów,
  3. Połączyć zdarzenia w logiczny łańcuch.

**Cel:**\
Zademonstrować, jak SIEM pozwala na szybką detekcję oraz tworzenie kontekstu zdarzeń.

***

### Materiały dodatkowe:

* MITRE ATT\&CK Matrix (np. T1059 – Command Line Execution),
* Sysinternals Suite (do analizy lokalnej),
* Strona [https://eventlogxp.com](https://eventlogxp.com/) – opisy ID zdarzeń Windows.

***

Poniżej znajdziesz gotowy **kod do uruchomienia lokalnie** – wygeneruje plik `wazuh_malicious_log_sample.csv` zawierający 200 zdarzeń, z czego ok. 30% to złośliwe aktywności (np. ransomware, C2, mimikatz, tworzenie kont itp.).

***

#### Kod Python do wygenerowania logów:

```python
import pandas as pd
from datetime import datetime, timedelta
import random
import uuid

# Ustawienia
start_time = datetime.now() - timedelta(days=1)
num_logs = 200

# Przykładowe dane
event_ids = [4625, 4624, 1, 3, 11, 7, 13, 4688, 7045, 4720]
usernames = ['admin', 'user1', 'john.doe', 'guest', 'attacker']
processes = ['cmd.exe', 'powershell.exe', 'explorer.exe', 'malware.exe', 'ransom.exe', 'mimikatz.exe', 'net.exe']
ip_addresses = ['192.168.1.10', '10.0.0.5', '172.16.0.2', '203.0.113.5', '45.33.32.156', '185.220.101.1']

# Złośliwe zdarzenia
malicious_events = [
    {"event_id": 1, "process": "ransom.exe", "description": "Suspicious process started (possible ransomware)"},
    {"event_id": 3, "process": "malware.exe", "description": "External C2 connection established"},
    {"event_id": 11, "process": "ransom.exe", "description": "Sensitive file modified by ransomware"},
    {"event_id": 7, "process": "malware.exe", "description": "Unusual DLL loaded by malware"},
    {"event_id": 13, "process": "powershell.exe", "description": "Suspicious registry key added"},
    {"event_id": 4688, "process": "mimikatz.exe", "description": "Credential dumping attempt (Mimikatz)"},
    {"event_id": 7045, "process": "net.exe", "description": "New service installed remotely"},
    {"event_id": 4720, "process": "net.exe", "description": "New user account created (potential persistence)"}
]

def generate_log(i):
    timestamp = start_time + timedelta(minutes=random.randint(0, 1440))
    is_malicious = random.random() < 0.3

    if is_malicious:
        ev = random.choice(malicious_events)
        event_id = ev["event_id"]
        process_name = ev["process"]
        event_message = ev["description"]
        username = 'attacker'
    else:
        event_id = random.choice(event_ids)
        process_name = random.choice(processes)
        username = random.choice(usernames)
        if event_id == 4625:
            event_message = f"Failed logon attempt for user {username}"
        elif event_id == 4624:
            event_message = f"Successful logon for user {username}"
        elif event_id == 1:
            event_message = f"Process {process_name} started"
        elif event_id == 3:
            event_message = f"Network connection established by {process_name}"
        elif event_id == 11:
            event_message = f"File modified by {process_name}"
        elif event_id == 7:
            event_message = f"DLL loaded by {process_name}"
        elif event_id == 13:
            event_message = f"Registry key created by {process_name}"
        elif event_id == 4688:
            event_message = f"New process created: {process_name}"
        elif event_id == 7045:
            event_message = f"New service installed by {process_name}"
        elif event_id == 4720:
            event_message = f"User account created via {process_name}"
        else:
            event_message = "Generic system event"

    source_ip = random.choice(ip_addresses)
    dest_ip = random.choice(ip_addresses)
    event_source = 'Sysmon' if event_id in [1, 3, 7, 11, 13, 4688] else 'Security'

    return {
        'timestamp': timestamp.strftime('%Y-%m-%d %H:%M:%S'),
        'event_id': event_id,
        'event_source': event_source,
        'username': username,
        'source_ip': source_ip,
        'dest_ip': dest_ip,
        'process_name': process_name,
        'event_message': event_message,
        'log_id': str(uuid.uuid4())
    }

logs = [generate_log(i) for i in range(num_logs)]
df = pd.DataFrame(logs)
df.to_csv("wazuh_malicious_log_sample.csv", index=False)
print("Plik zapisany jako: wazuh_malicious_log_sample.csv")
```

***

**Gotowy zestaw reguł Wazuh**, który pozwoli wykrywać złośliwe działania wygenerowane w pliku logów, który wcześniej omawialiśmy. Są to reguły niestandardowe (`local_rules.xml`), które możesz wgrać do katalogu `/var/ossec/etc/rules/local_rules.xml` i przeładować Wazuh.

***

### Plik: `/var/ossec/etc/rules/local_rules.xml`

```xml
<group name="custom,sysmon,windows">
  <!-- Ransomware: uruchomienie podejrzanego procesu -->
  <rule id="100100" level="10">
    <if_sid>61603</if_sid> <!-- Sysmon Event ID 1 -->
    <match>ransom.exe</match>
    <description>Ransomware detected: ransom.exe process started</description>
  </rule>

  <!-- C2 Communication -->
  <rule id="100101" level="10">
    <if_sid>61605</if_sid> <!-- Sysmon Event ID 3 -->
    <match>malware.exe</match>
    <description>Possible C2 connection from malware.exe</description>
  </rule>

  <!-- Zmiana plików przez ransomware -->
  <rule id="100102" level="9">
    <if_sid>61609</if_sid> <!-- Sysmon Event ID 11 -->
    <match>ransom.exe</match>
    <description>File modified by ransomware</description>
  </rule>

  <!-- DLL Injection -->
  <rule id="100103" level="8">
    <if_sid>61607</if_sid> <!-- Sysmon Event ID 7 -->
    <match>malware.exe</match>
    <description>DLL injection by malware.exe</description>
  </rule>

  <!-- Podejrzana edycja rejestru -->
  <rule id="100104" level="7">
    <if_sid>61613</if_sid> <!-- Sysmon Event ID 13 -->
    <match>powershell.exe</match>
    <description>Suspicious registry modification by PowerShell</description>
  </rule>

  <!-- Mimikatz execution -->
  <rule id="100105" level="10">
    <if_sid>18107</if_sid> <!-- Windows Security ID 4688 -->
    <match>mimikatz.exe</match>
    <description>Credential dumping tool detected (Mimikatz)</description>
  </rule>

  <!-- Tworzenie usługi (Persistence) -->
  <rule id="100106" level="8">
    <if_sid>18109</if_sid> <!-- Event ID 7045 -->
    <match>net.exe</match>
    <description>New service installed remotely (possible persistence)</description>
  </rule>

  <!-- Tworzenie konta użytkownika (Persistence) -->
  <rule id="100107" level="8">
    <if_sid>18112</if_sid> <!-- Event ID 4720 -->
    <match>net.exe</match>
    <description>New user account created - possible attacker persistence</description>
  </rule>

  <!-- Failed logon brute-force -->
  <rule id="100108" level="5" frequency="5" timeframe="60">
    <if_sid>18107</if_sid> <!-- Event ID 4625 -->
    <description>Multiple failed logon attempts - brute-force attack</description>
    <group>authentication_failed, brute_force</group>
  </rule>
</group>
```

***

### Co musisz zrobić:

1.  **Edytuj plik z regułami Wazuh**:

    ```bash
    sudo nano /var/ossec/etc/rules/local_rules.xml
    ```
2. **Wklej powyższy kod XML** i zapisz plik.
3.  **Sprawdź poprawność składni XML**:

    ```bash
    /var/ossec/bin/wazuh-logtest
    ```
4.  **Zrestartuj Wazuh managera**:

    ```bash
    sudo systemctl restart wazuh-manager
    ```

***

### ✅ Co wykrywają te reguły:

| ID Reguły | Wykrywane zachowanie                       | Poziom | Proces         |
| --------- | ------------------------------------------ | ------ | -------------- |
| 100100    | Ransomware (uruchomienie)                  | 10     | ransom.exe     |
| 100101    | Komunikacja C2                             | 10     | malware.exe    |
| 100102    | Modyfikacja plików przez ransomware        | 9      | ransom.exe     |
| 100103    | DLL Injection                              | 8      | malware.exe    |
| 100104    | Zmiana rejestru przez PowerShell           | 7      | powershell.exe |
| 100105    | Uruchomienie Mimikatz                      | 10     | mimikatz.exe   |
| 100106    | Instalacja nowej usługi                    | 8      | net.exe        |
| 100107    | Tworzenie konta użytkownika                | 8      | net.exe        |
| 100108    | Brute-force (>=5 nieudanych logowań / 60s) | 5      | dowolny        |

***

Poniżej znajdziesz **gotowe konfiguracje** do integracji Wazuh z systemami alertowania: **e-mail, Slack, Filebeat (ElasticSearch)** i importem dashboardu do **Kibany**. Możesz je ręcznie wkleić do odpowiednich plików konfiguracyjnych.

***

### E-mail alerty (dla zdarzeń z poziomem ≥ 9)

**Plik:** `/var/ossec/etc/ossec.conf`

```xml
<global>
  <email_notification>yes</email_notification>
  <smtp_server>smtp.twojadomena.pl</smtp_server>
  <email_from>wazuh@twojadomena.pl</email_from>
  <email_to>soc@twojadomena.pl</email_to>
  <email_maxperhour>12</email_maxperhour>
</global>

<rule_alert>
  <level>9</level>
  <email_alert>yes</email_alert>
</rule_alert>
```

***

### Slack (integracja z webhookiem Slacka)

**Plik:** `/var/ossec/integrations/slack`

```json
{
  "hook_url": "https://hooks.slack.com/services/TOKEN/TOKEN/ID",
  "level": 9,
  "alert_format": "json"
}
```

**Dodaj do ossec.conf:**

```xml
<integration>
  <name>slack</name>
  <hook_url>https://hooks.slack.com/services/TOKEN/TOKEN/ID</hook_url>
  <level>9</level>
</integration>
```

***

### Filebeat → Elasticsearch → Kibana

**Plik:** `/etc/filebeat/filebeat.yml`

```yaml
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/ossec/logs/alerts/alerts.json

output.elasticsearch:
  hosts: ["http://localhost:9200"]
  username: "elastic"
  password: "haslo"

setup.kibana:
  host: "localhost:5601"
```

***

### Kibana dashboard (wizualizacja alertów)

**Co zrobić:**

1. Zainstaluj plugin Wazuh w Kibanie:\
   &#x20;[https://documentation.wazuh.com/current/kibana-app/](https://documentation.wazuh.com/current/kibana-app/)
2. Użyj gotowych dashboardów Wazuh lub zaimportuj swój (z JSON-a).
3.  Przykładowy filtr:

    ```kibana
    rule.level >= 9 AND agent.name : "windows_host_1"
    ```

***



Oto **gotowy szablon integracji Wazuh z Discordem** za pomocą webhooka, który pozwala wysyłać alerty (np. te powyżej level 9) bezpośrednio na Twój kanał Discord.

***

### 1. Stwórz webhooka w Discordzie

1. Otwórz **Discord** i przejdź do kanału, gdzie chcesz otrzymywać alerty.
2. Kliknij **Ustawienia kanału → Integracje → Webhooki → Nowy webhook**.
3. Skopiuj **URL webhooka**, np. `https://discord.com/api/webhooks/xxx/yyy`.

***

### 2. Utwórz skrypt integracyjny w Wazuh

**Plik:** `/var/ossec/integrations/discord`

```bash
#!/bin/bash

# Wazuh to Discord alert integration
# Ustaw swój Webhook URL poniżej:
WEBHOOK_URL="https://discord.com/api/webhooks/xxx/yyy"

read input
ALERT=$(echo $input | jq -r '.rule.description + " | Agent: " + .agent.name + " | " + .full_log')

curl -H "Content-Type: application/json" -X POST \
-d "{\"content\": \"🚨 Wazuh Alert:\n$ALERT\"}" \
"$WEBHOOK_URL"

exit 0
```

Ustaw prawa do wykonania:

```bash
chmod +x /var/ossec/integrations/discord
```

***

### 3. Dodaj integrację do `ossec.conf`

**Plik:** `/var/ossec/etc/ossec.conf`

W sekcji `<integration>` dodaj:

```xml
<integration>
  <name>discord</name>
  <hook_url>https://discord.com/api/webhooks/xxx/yyy</hook_url>
  <level>9</level>
  <alert_format>json</alert_format>
</integration>
```

***

### 4. Zrestartuj Wazuh managera

```bash
sudo systemctl restart wazuh-manager
```

***

### 5. (Opcjonalnie) Test alertu

Możesz ręcznie przetestować, przekazując testowy JSON:

```bash
/var/ossec/integrations/discord < /var/ossec/logs/alerts/alerts.json
```

***

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

**Kluczowe wskaźniki kompromitacji (IoC)** oraz anomalie, na które powinieneś zwracać uwagę jako analityk SOC lub operator SIEM. Te zdarzenia powinny wzbudzić alert i reakcję, szczególnie w środowisku z SIEM jak **Wazuh**, **ELK**, **Splunk** czy **QRadar**.

***

### **Na co zwracać uwagę – podejrzane sytuacje i włamania:**

#### 1. **Nieudane logowania (brute-force, spray):**

* 🔹 Wiele błędnych logowań (np. 4625 – Windows).
* 🔹 Próby logowania na konta uprzywilejowane (admin, domain admin, root).
* 🔹 Logowania z nietypowych lokalizacji lub godzin.

**Reakcja:**

* Zablokuj adresy IP.
* Sprawdź konta próbujące logowań.
* Wdróż MFA / rate limiting.

***

#### 2. **Logowania poza godzinami pracy (tzw. after-hours activity):**

* 🔹 Logowanie np. w nocy, weekend.
* 🔹 Aktywność z nietypowych hostów lub geolokalizacji.

**Reakcja:**

* Powiadom zespół bezpieczeństwa.
* Porównaj z planowanymi zadaniami.
* Weryfikuj użytkownika (SOC Level 1 → eskalacja).

***

#### 3. **Uruchomienie złośliwych procesów:**

* 🔹 `mimikatz.exe`, `ransom.exe`, `net.exe`, `powershell.exe` z parametrami typu `-enc`, `Invoke-Expression`, `DownloadString()`.
* 🔹 Nietypowe procesy uruchamiane przez zwykłych użytkowników.

**Reakcja:**

* Zidentyfikuj proces i właściciela.
* Zatrzymaj proces, przeanalizuj ślad (Sysmon Event ID 1).
* Przeskanuj host.

***

#### 4. **Połączenia do Command & Control (C2):**

* 🔹 Sysmon Event ID 3: połączenia wychodzące do znanych C2 (np. na nietypowych portach: 443, 53, 8080).
* 🔹 Komunikacja z adresami IP spoza organizacji.

**Reakcja:**

* Zablokuj ruch sieciowy (firewall, proxy).
* Prześledź źródło (host, proces).
* Przeanalizuj payload.

***

#### 5. **Zmiany w rejestrze systemowym / tworzenie usług:**

* 🔹 Zmiany startup keys w rejestrze (`Run`, `RunOnce`) – persistence.
* 🔹 Instalacja usług (7045) lub harmonogramów zadań.
* 🔹 Użytkownik `attacker` tworzy usługę.

**Reakcja:**

* Cofnij zmiany w rejestrze.
* Usuń podejrzane usługi.
* Przeskanuj host AV/EDR.

***

#### 6. **Tworzenie nowych kont użytkowników:**

* 🔹 Event ID 4720 – nowe konto utworzone.
* 🔹 Zwłaszcza przez `net.exe` lub PowerShell.

**Reakcja:**

* Usuń nieautoryzowane konta.
* Przeanalizuj, kto i skąd utworzył konto.
* Wdróż alertowanie o tworzeniu kont.

***

#### 7. **Szyfrowanie plików / masowe zmiany nazw:**

* 🔹 Wzrost liczby zdarzeń typu "modified" (Sysmon ID 11).
* 🔹 Podejrzane rozszerzenia: `.locked`, `.enc`, `.crypt`.

**Reakcja:**

* Odizoluj host.
* Zidentyfikuj źródło ransomware.
* Odtwórz dane z backupu.

***

#### 8. **Eksfiltracja danych:**

* 🔹 Nietypowe użycie `curl`, `scp`, `ftp`, `powershell Invoke-WebRequest`.
* 🔹 Wysyłka dużych ilości danych do zewnętrznych adresów.

**Reakcja:**

* Monitoruj przepływy sieciowe.
* Zatrzymaj transfer.
* Zbadaj źródło danych i użytkownika.

***

#### 9. **Alerty korelowane (kontekst SIEM):**

* 🔹 Prób logowania + uruchomienie Powershella + komunikacja sieciowa = **atak lateralny**.
* 🔹 Zmiana w rejestrze + stworzenie konta + uruchomienie Mimikatz = **pełna faza ataku MITRE TTP**.

**Reakcja:**

* Koreluj logi – z pomocą reguł SIEM lub Sigma.
* Eskaluj alerty z poziomu 7+.
* Aktywuj procedury IR (incident response).

***

### **Jak reagować – zalecane kroki (SOC Tier 1/2):**

| Poziom zagrożenia | Działania                                          |
| ----------------- | -------------------------------------------------- |
| **Niski (1–4)**   | Obserwuj, oznacz jako false positive / do analizy  |
| **Średni (5–8)**  | Analiza, eskalacja do Tier 2, sprawdź host/logi    |
| **Wysoki (9–15)** | Izolacja hosta, eskalacja IR, zbieranie artefaktów |

***

### Dodatkowe wskazówki:

* Stosuj **reguły korelacyjne** (np. 3 błędy logowania + 1 sukces = podejrzane).
* Obserwuj **geolokalizację adresów IP**.
* Twórz alerty na **nietypowe pliki, procesy i rejestr**.
* Zbieraj logi z wielu źródeł: endpoint, sieć, AD, firewall.
* Używaj narzędzi typu **Sigma, MITRE ATT\&CK, OpenCTI** do wzbogacenia detekcji.

***

#### Kod do wygenerowania checklisty PDF:

```python
from fpdf import FPDF

class PDF(FPDF):
    def header(self):
        self.set_font('Arial', 'B', 12)
        self.cell(0, 10, 'Checklist: Wykrywanie i Reakcja na Incydenty (SOC/SIEM)', 0, 1, 'C')
        self.ln(5)

    def chapter_title(self, title):
        self.set_font('Arial', 'B', 11)
        self.set_fill_color(240, 240, 240)
        self.cell(0, 8, title, 0, 1, 'L', 1)
        self.ln(2)

    def chapter_body(self, text):
        self.set_font('Arial', '', 10)
        self.multi_cell(0, 5, text)
        self.ln()

pdf = PDF()
pdf.add_page()

pdf.chapter_title("🔍 Podejrzane zdarzenia do wykrycia (przykłady reguł SIEM)")
pdf.chapter_body("""
1. Nieudane logowania (Event ID 4625) – brute-force, spray.
2. Logowania poza godzinami pracy (weekend, noc).
3. Uruchomienie procesów typu: mimikatz.exe, ransom.exe, powershell.exe.
4. Połączenia wychodzące do znanych adresów C2 (Sysmon ID 3).
5. Modyfikacja rejestru systemowego (Sysmon ID 13).
6. Tworzenie nowych usług (7045) lub użytkowników (4720).
7. Modyfikacja plików i wzorce ransomware (Sysmon ID 11).
8. Eksfiltracja danych – narzędzia sieciowe (curl, ftp, Invoke-WebRequest).
9. Korelowane zdarzenia (np. logon + powershell + sieć).
""")

pdf.chapter_title("🛡️ Reakcje na alerty (SOC Tier 1 i Tier 2)")
pdf.chapter_body("""
- Poziom 1–4: Obserwacja, klasyfikacja jako false positive (jeśli potwierdzony).
- Poziom 5–8: Analiza kontekstowa, sprawdzenie hosta, eskalacja do Tier 2.
- Poziom 9–15: Izolacja hosta, powiadomienie CSIRT, zabezpieczenie logów i artefaktów.
""")

pdf.chapter_title("📌 Dobre praktyki")
pdf.chapter_body("""
✓ Koreluj wiele źródeł (Windows, Sysmon, firewall, AD).
✓ Monitoruj zmiany w rejestrze, usługach, kontach użytkowników.
✓ Twórz reguły detekcyjne na podstawie MITRE ATT&CK.
✓ Filtruj logi po nazwach procesów, adresach IP i nazwach hostów.
✓ Zgłaszaj anomalie czasowe (np. logon w nocy, transfer danych nocą).
""")

pdf.chapter_title("📋 Narzędzia wspierające")
pdf.chapter_body("""
• Sigma rules: https://sigmahq.io
• Wazuh rules: /var/ossec/etc/rules/local_rules.xml
• MITRE ATT&CK: https://attack.mitre.org
• OpenCTI: https://www.opencti.io
""")

pdf.output("SOC_SIEM_Checklista_Wykrywania_Reakcji.pdf")
print("Plik zapisany jako: SOC_SIEM_Checklista_Wykrywania_Reakcji.pdf")
```

***

Po uruchomieniu powstanie plik:\
📄 `SOC_SIEM_Checklista_Wykrywania_Reakcji.pdf`



