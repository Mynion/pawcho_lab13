# Laboratorium 13 – LEMP Stack (Docker Compose)

## 1. Opis projektu

Projekt przedstawia uruchomienie stosu LEMP (Linux, Nginx, MySQL, PHP) z dodatkowym narzędziem phpMyAdmin w środowisku Docker Compose.

Aplikacja składa się z 4 mikrousług:

- Nginx (serwer WWW)
- PHP-FPM (backend PHP)
- MySQL (baza danych)
- phpMyAdmin (interfejs administracyjny bazy danych)

Dodatkowo zastosowano:
- sieci frontend/backend
- healthchecki dla usług
- Docker Secrets do przechowywania danych wrażliwych

---

## 2. Uruchomienie projektu

### Budowa i uruchomienie kontenerów
```
docker compose up -d
```
<img width="1461" height="212" alt="Zrzut ekranu 2026-06-15 175959" src="https://github.com/user-attachments/assets/ad9551f7-77b9-450c-a87c-30885e7fec3f" />

### Sprawdzenie statusu kontenerów
```
docker ps
```
<img width="1788" height="117" alt="Zrzut ekranu 2026-06-15 180017" src="https://github.com/user-attachments/assets/51c12b07-aa93-4193-94c5-b46a874d7480" />

### Sprawdzenie sieci
```
docker network ls
```
<img width="574" height="191" alt="image" src="https://github.com/user-attachments/assets/5047d1f5-7f30-41d4-9b1e-056a09ca4cc4" />

```
docker network inspect lemp-stack_backend
```
<img width="1163" height="961" alt="Zrzut ekranu 2026-06-15 180130" src="https://github.com/user-attachments/assets/e30911af-e015-45ef-89af-07102714ab60" />
<img width="1025" height="558" alt="Zrzut ekranu 2026-06-15 180214" src="https://github.com/user-attachments/assets/f509b320-3459-4912-8e30-bd3ca875a542" />

```
docker network inspect lemp-stack_frontend
```
<img width="1163" height="922" alt="Zrzut ekranu 2026-06-15 180230" src="https://github.com/user-attachments/assets/8ac64400-3ed5-40b0-8727-a142d054e39d" />
<img width="1163" height="321" alt="Zrzut ekranu 2026-06-15 180244" src="https://github.com/user-attachments/assets/c81d7652-0b14-4602-bb53-494e32f2fd6d" />

---

## 3. Dostęp do aplikacji

### Nginx (LEMP)

http://localhost:4001

<img width="1915" height="977" alt="Zrzut ekranu 2026-06-15 180300" src="https://github.com/user-attachments/assets/99e232aa-6808-47b9-8fdd-532bf962df23" />

---

### phpMyAdmin

http://localhost:6001

<img width="1908" height="947" alt="Zrzut ekranu 2026-06-15 180320" src="https://github.com/user-attachments/assets/aef4f1e9-eb9d-413d-97ad-9b268940e6ff" />

---

## 4. Tworzenie testowej bazy danych

Zalogowano jako root:

<img width="697" height="228" alt="Zrzut ekranu 2026-06-15 180801" src="https://github.com/user-attachments/assets/070d2b93-fd61-4acb-a50b-c35695d36e24" />
<img width="1503" height="543" alt="image" src="https://github.com/user-attachments/assets/66b3bef5-b7c0-4fe6-a3e8-7599d9e341ac" />



Zalogowano jako user:

<img width="1397" height="377" alt="image" src="https://github.com/user-attachments/assets/c734df0a-aeb8-4de8-af63-919f2f7f866d" />

---

## 5. Docker Secrets

Sekrety:
- db_root_password
- db_password

Sprawdzenie:
```
docker exec -it lemp-stack-mysql-1 cat /run/secrets/db_root_password
```
```
docker exec -it lemp-stack-mysql-1 cat /run/secrets/db_password
```
<img width="1082" height="71" alt="Zrzut ekranu 2026-06-15 181348" src="https://github.com/user-attachments/assets/a62c9bf6-4d60-4107-a468-74c8968de9b0" />

---

## 6. Healthcheck

MySQL, PHP i Nginx posiadają healthchecki.

---

## 7. Wnioski

LEMP działa poprawnie z separacją sieci, secrets i healthcheckami.
