# Bezpieczeństwo w chmurze - w pytaniach i odpowiedziach

Test wielokrotnego wyboru (MCQ)

1. Kto odpowiada za dane w modelu chmury? \
   A. Dostawca B. Użytkownik ✅, C. Nikt D. Audytor
2. Zero Trust oznacza: \
   A. Brak zabezpieczeń B. Zaufanie sieci wewnętrznej C. Weryfikację każdego dostępu ✅, D. Szyfrowanie tylko danych
3. Least privilege to: \
   A. Maksymalne uprawnienia B. Minimalne wymagane uprawnienia ✅, C. Brak kontroli dostępu D. Tylko dla adminów
4. Gdzie użytkownik ma NAJWIĘCEJ odpowiedzialności? \
   A. SaaS B. PaaS C. IaaS ✅, D. FaaS
5. Defense in Depth oznacza: \
   A. Jedną warstwę ochrony B. Brak ochrony C. Wiele warstw zabezpieczeń ✅, D. Tylko firewall
6. Co najlepiej zabezpiecza dostęp? \
   A. Hasło „abc1234!%\*” B. MFA ✅, C. Brak logowania D. Publiczny dostęp
7. Najczęstszy błąd w chmurze: \
   A. Za dużo logów B. Publiczne zasoby ✅, C. Za mało danych D. Za szybkie serwery
8. Co służy do wykrywania incydentów? \
   A. SIEM ✅, B. Word C. Excel D. DNS
9. Szyfrowanie TLS dotyczy: \
   A. danych w spoczynku, B. danych w transmisji ✅, C. backupów D. CPU
10. DevSecOps to: \
    A. brak bezpieczeństwa B. integracja security w DevOps ✅, C. tylko testy ręczne D. tylko firewall
11. Który standard dotyczy bezpieczeństwa informacji? A. HTTP B. FTP C. ISO 27001 ✅, D. HTML
12. Security Groups działają: \
    A. globalnie B. na poziomie instancji ✅, C. tylko offline D. tylko w SaaS
13. KMS służy do: \
    A. zarządzania użytkownikami B. zarządzania kluczami szyfrowania ✅, C. backupu D. sieci
14. Najlepsza praktyka IAM: \
    A. jedno konto dla wszystkich B. brak MFA C. role i least privilege ✅, D. publiczny dostęp
15. W SaaS użytkownik odpowiada za: \
    A. serwery, B. sieć, C. dane i dostęp ✅, D. hardware

***

PYTANIE I ODPOWIEDZ:

1.

Pytanie: Wyjaśnij różnice w odpowiedzialności bezpieczeństwa między IaaS, PaaS i SaaS na przykładzie incydentu.

Odpowiedź: W IaaS użytkownik odpowiada za system operacyjny, konfigurację i dane, więc np. wyciek danych z powodu braku aktualizacji OS jest jego winą. W PaaS użytkownik odpowiada głównie za aplikację i dane – wyciek może wynikać np. z błędu w kodzie. W SaaS dostawca zarządza całą infrastrukturą, ale użytkownik nadal odpowiada za dostęp i dane – np. wyciek przez słabe hasło lub brak MFA.

2.

Pytanie: Dlaczego Zero Trust jest ważniejszy w chmurze niż on-premise?

Odpowiedź: Bo w chmurze nie ma wyraźnej granicy sieci (perimeter). Zasoby są dostępne przez Internet, więc każde żądanie musi być weryfikowane. Zero Trust eliminuje założenie, że „wewnętrzne = bezpieczne”.

3.

Pytanie: Jakie konsekwencje ma brak least privilege?

Odpowiedź: Zbyt szerokie uprawnienia umożliwiają eskalację ataku – przejęte konto może uzyskać dostęp do całej infrastruktury, usunąć dane lub je wyeksportować.

4.

Pytanie: Zaprojektuj bezpieczny dostęp administratora.

Odpowiedź: Administrator powinien korzystać z IAM ról zamiast kont stałych, mieć obowiązkowe MFA, dostęp tylko z zaufanych lokalizacji (np. VPN), a wszystkie działania powinny być logowane i monitorowane (SIEM, alerty).

5.

Pytanie: Różnice: at rest vs in transit?

Odpowiedź:

At rest – dane zapisane (np. dysk), chroni przed kradzieżą fizyczną lub dostępem do storage In transit – dane w przesyle (TLS), chroni przed podsłuchem (MITM)&#x20;

6\.

Pytanie: Jak misconfiguration prowadzi do ataku?

Odpowiedź: Np. publiczny bucket storage bez autoryzacji → każdy może pobrać dane. To jeden z najczęstszych realnych incydentów.

7.

Pytanie: Security groups vs firewall?

Odpowiedź: Security groups działają na poziomie instancji (kontrola ruchu do VM), są stateful. Firewall działa szerzej – może kontrolować cały ruch sieciowy i mieć bardziej zaawansowane reguły.

8.

Pytanie: Proces wykrywania i reagowania?

Odpowiedź: Zbieranie logów → analiza (SIEM) → wykrycie anomalii → alert → reakcja (np. blokada konta) → analiza incydentu i poprawa zabezpieczeń.

9.

Pytanie: Elementy bezpiecznej architektury?

Odpowiedź: IAM, MFA, segmentacja sieci, szyfrowanie danych, monitoring, backupy, automatyzacja (IaC), audyty.

10.

Pytanie: DevSecOps – rola i przykład?

Odpowiedź: To integracja bezpieczeństwa w procesie DevOps. Np. automatyczne skanowanie kodu (SAST) i konfiguracji przed wdrożeniem w CI/CD.

11.

Pytanie: Jak działa KMS/HSM?

Odpowiedź: KMS zarządza kluczami szyfrowania (tworzenie, rotacja, dostęp), a HSM przechowuje je w bezpiecznym sprzęcie. Chroni to dane przed nieautoryzowanym odszyfrowaniem.

12.

Pytanie: Dlaczego IAM jest najważniejszy?

Odpowiedź: Bo kontroluje dostęp do wszystkiego. Nawet najlepsze zabezpieczenia nie działają, jeśli atakujący przejmie konto z wysokimi uprawnieniami.
