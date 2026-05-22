# Dzień 1 - linux i sieci

## 1. Linux - system plików

Linux traktuje wszystko jako plik.

Struktura:

```
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── srv
├── sys
├── tmp
├── usr
└── var
```

Najważniejsze katalogi:

| Katalog | Przeznaczenie          |
| ------- | ---------------------- |
| /       | katalog główny         |
| /home   | pliki użytkowników     |
| /root   | konto administratora   |
| /etc    | konfiguracja systemu   |
| /var    | logi i dane aplikacji  |
| /tmp    | pliki tymczasowe       |
| /usr    | programy użytkownika   |
| /bin    | podstawowe komendy     |
| /proc   | informacje o procesach |
|         |                        |

pwd - pokazuje aktualny katalog\
ls -la - lista plików\
cd /etc - zmiana katalogu\
mkdir test - tworzenie katalogu\
touch plik.txt - tworzenie pliku\
chmod:\
Służy do zmiany uprawnień.

Linux posiada:

```
r = read = 4w = write = 2x = execute = 1
```

Dla:

```
u = właścicielg = grupao = inni
```

Przykład:

```
chmod 755 skrypt.sh
```

oznacza:

```
7 = rwx5 = r-x5 = r-x
```

Właściciel może wszystko.

Inni tylko czytać i uruchamiać.

Bardzo ważne:

```
chmod 600 ~/.ssh/id_rsa
```

Klucz prywatny SSH.\
\
chown - zmiana właściciela\
ls - l

```
sudo chown jan:developers plik.txt
```

gdzie:

```
jan = użytkownikdevelopers = grupa
```

Rekursywnie:

```
sudo chown -R www-data:www-data /var/www
```

Bardzo częste przy serwerach www

grep - wyszukiwanie tekstów

Przykład:

```
grep root /etc/passwd
```

Wyszuka:

```
root:x:0:0:root:/root:/bin/bash
```

Ignorowanie wielkości liter:

```
grep -i error log.txt
```

Rekursywnie:

```
grep -r password .
```

Przydatne przy analizie logów.

SSH = bezpieczne zdalne logowanie.

Instalacja:

```
sudo apt updatesudo apt install openssh-server
```

Sprawdzenie:

```
systemctl status ssh
```

Połączenie:

```
ssh user@192.168.1.100
```

***

## Bezpieczna konfiguracja SSH

Plik:

```
sudo nano /etc/ssh/sshd_config
```

Ustaw:

```
PermitRootLogin noPasswordAuthentication noPubkeyAuthentication yes
```

Restart:

```
sudo systemctl restart ssh
```

***

## Generowanie kluczy

Na komputerze klienta:

```
ssh-keygen -t ed25519
```

Powstanie:

```
id_ed25519id_ed25519.pub
```

Kopiowanie klucza:

```
ssh-copy-id user@IP
```

Logowanie:

```
ssh user@IP
```

Bez hasła.

To jest obecnie rekomendowana metoda.

## SCP

Bezpieczne kopiowanie przez SSH.

Kopiowanie pliku:

```
scp plik.txt user@192.168.1.100:/home/user/
```

Pobranie:

```
scp user@192.168.1.100:/home/user/log.txt .
```

Katalog:

```
scp -r backup/ user@IP:/backup
```

***

## systemd

Zarządza usługami.

Lista:

```
systemctl list-units
```

Start:

```
sudo systemctl start nginx
```

Stop:

```
sudo systemctl stop nginx
```

Restart:

```
sudo systemctl restart nginx
```

Status:

```
systemctl status nginx
```

Autostart:

```
sudo systemctl enable nginx

```

### TCP/IP

IP identyfikuje host.

Przykład:

```
192.168.1.10
```

TCP:

* niezawodny
* kontrola błędów
* retransmisja

Przykłady:

```
HTTPSSSHSMTP
```

UDP:

* szybszy
* bez potwierdzeń

Przykłady:

```
DNSVoIPStreaming
```

***

### DNS

Tłumaczy nazwę na adres IP.

Przykład:

```
google.com↓142.250.x.x
```

Sprawdzenie:

```
dig google.com
```

lub

```
nslookup google.com
```

### HTTPS

HTTP + TLS.

Port:

```
443
```

Zapewnia:

* poufność
* integralność
* uwierzytelnienie

### NAT

Pozwala wielu urządzeniom używać jednego publicznego IP.

Przykład:

```
LaptopTelefonTV↓Router↓Internet
```

Domowe routery używają NAT praktycznie zawsze.

***

### VPN

Tworzy szyfrowany tunel.

Przykład:

```
Laptop ↓VPN Tunnel ↓Firma
```

Popularne:

* WireGuard
* OpenVPN

***

### SSL/TLS

TLS jest następcą SSL.

Dzisiaj używa się:

```
TLS 1.2TLS 1.3
```

Sprawdzenie certyfikatu:

```
openssl s_client -connect google.com:443
```



## Konfiguracja SSH krok po kroku

Na VM:

```
sudo apt install openssh-server -y
```

Sprawdź:

```
systemctl status ssh
```

Adres IP:

```
ip addr
```

Na komputerze lokalnym:

```
ssh-keygen -t ed25519
```

Następnie:

```
ssh-copy-id user@IP_VM
```

Połącz:

```
ssh user@IP_VM
```

Wyłącz logowanie hasłem:

```
sudo nano /etc/ssh/sshd_config
```

Ustaw:

```
PasswordAuthentication noPermitRootLogin no
```

Restart:

```
sudo systemctl restart ssh


```

## Prosty skrypt backupu

```
#!/bin/bash
SOURCE="/home/user/dane"
BACKUP="/home/user/backups"
DATE=$(date +%Y-%m-%d_%H-%M)
mkdir -p "$BACKUP"
tar -czf "$BACKUP/backup_$DATE.tar.gz" "$SOURCE"
echo "Backup wykonany: $DATE"
```

Nadaj prawa:

```
chmod +x backup.sh
```

Uruchom:

```
./backup.sh
```

Sprawdzenie:

```
ls backups
```

Otworz crontab: \
crontab -e

Dodaj zadanie: \
0 18 \* \* \* /home/user/scripts/backup.sh

Zapis logów:\
0 18 \* \* \* /home/user/scripts/backup.sh >> /home/user/logs/backup.log 2>&1

Sprawdź zapisane zadania: \
crontab -l

