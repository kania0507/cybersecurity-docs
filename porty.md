# PORTY

NAJPOPULARNIEJSZE PORTY (szyfrowane i nieszyfrowane razem)

WWW / APLIKACJE WEBOWE\
HTTP – 80 (nieszyfrowany)\
HTTPS – 443 (szyfrowany TLS)\
HTTP-alt – 8080\
HTTPS-alt – 8443

POCZTA

SMTP – 25 (nieszyfrowany, głównie serwer–serwer)\
SMTP Submission – 587 (STARTTLS, obecny standard dla klientów)\
SMTPS – 465 (SSL/TLS)

POP3 – 110 (nieszyfrowany)\
POP3S – 995 (SSL/TLS)

IMAP – 143 (nieszyfrowany)\
IMAPS – 993 (SSL/TLS)

BAZY DANYCH

MySQL – 3306 (SSL opcjonalnie)\
PostgreSQL – 5432 (SSL opcjonalnie)\
MSSQL – 1433 (TLS opcjonalnie)\
Oracle – 1521\
MongoDB – 27017\
Redis – 6379

ZDALNY DOSTĘP

SSH – 22 (szyfrowany)\
Telnet – 23 (nieszyfrowany, przestarzały)\
RDP – 3389 (TLS)\
VNC – 5900 (domyślnie nieszyfrowany)

TRANSFER PLIKÓW

FTP – 21 (nieszyfrowany)\
FTPS – 990 (SSL/TLS)\
SFTP – 22 (przez SSH)\
TFTP – 69 UDP

USŁUGI SIECIOWE

DNS – 53 TCP/UDP\
DHCP – 67/68 UDP\
SNMP – 161 UDP\
LDAP – 389\
LDAPS – 636\
SMB – 445\
Kerberos – 88\
NTP – 123 UDP

***

MINI ŚCIĄGA – JAK SPRAWDZIĆ CO DZIAŁA NA JAKIM PORCIE

WINDOWS

1. Sprawdź nasłuchujące porty:\
   netstat -ano | find "LISTEN"
2. Sprawdź jaki program używa PID:\
   tasklist | findstr NUMER\_PID
3. PowerShell (czytelniej):\
   Get-NetTCPConnection -State Listen

LINUX

1. Najlepiej:\
   sudo ss -tulpn
2. Alternatywa:\
   sudo lsof -i -P -n

macOS

lsof -i -P -n

SPRAWDZENIE Z ZEWNĄTRZ (czy port jest wystawiony do internetu)

nmap TWOJE\_IP\
nmap -p 1433 TWOJE\_IP

***

