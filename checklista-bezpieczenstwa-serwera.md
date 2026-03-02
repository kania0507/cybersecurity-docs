# CHECKLISTA BEZPIECZEŃSTWA SERWERA

1. Aktualizacje

* System operacyjny aktualny
* Aktualne poprawki bezpieczeństwa
* Aktualne wersje usług (Apache/Nginx, MySQL, MSSQL itd.)

2. Otwarte porty

* Sprawdzone poleceniem ss/netstat
* Wystawione tylko te, które są potrzebne
* Brak publicznego dostępu do baz danych (3306, 5432, 1433)
* Brak publicznego dostępu do SMB (445)
* RDP (3389) dostępny tylko przez VPN

3. Firewall

* Włączony firewall (Windows Firewall / ufw / iptables)
* Zasada „deny all, allow only needed”
* Ograniczenia IP dla SSH i paneli administracyjnych

4. SSH

* Wyłączone logowanie root
* Zmieniony port (opcjonalnie)
* Logowanie kluczem zamiast hasła
* Fail2ban lub podobne zabezpieczenie

5. Hasła i konta

* Silne hasła
* Wyłączone nieużywane konta
* Zasada najmniejszych uprawnień
* MFA tam gdzie możliwe

6. Certyfikaty

* HTTPS wymuszony
* Aktualny certyfikat TLS
* Wyłączone stare protokoły (SSLv3, TLS 1.0)

7. Monitoring i logi

* Włączone logowanie zdarzeń
* Regularna kontrola logów
* Monitoring prób logowania
* Alerty o nietypowej aktywności

8. Kopie zapasowe

* Regularne backupy
* Backup poza serwerem (off-site)
* Test przywracania danych

9. Usługi zbędne

* Wyłączone nieużywane serwisy
* Usunięte domyślne aplikacje
* Zamknięte porty testowe (np. 8080 jeśli niepotrzebny)

10. Test bezpieczeństwa

* Skan nmap z zewnątrz
* Skan podatności (np. OpenVAS)
* Sprawdzenie konfiguracji TLS
