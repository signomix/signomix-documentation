# Przesyłanie danych przez REST API

Poniższe przykłady dotyczą urządzeń typu HTTP (nazywanych też w dokumentacji Generic lub Direct). Takie 
urządzenia powinny mieć możliwość wysyłania zapytań HTTP bezpośrednio do API Signomiksa.

W zależności od implementacji urządzenie tego typu może ignorować otrzymaną odpowiedź lub ją odbierać i analizować.

Treść odpowiedzi może zawierać polecenie, które urządzenie może odpowiednio zinterpretować.

Adresy metod API dla urządzeń HTTP dzielą się na dwie grupy, różniące się sposobem interpretacji żądania:
- adresy kończące się na `/io` przesyłają dane do przetworzenia, a kod odpowiedzi wynika ze stanu (poprawności) przetworzenia tych danych.
- adresy kończące się na `in` przesyłają dane do przetworzenia, ale zwracają odpowiedź przed rozpoczęciem przetwarzania tych danych.

Obydwa typy adresów mogą zwrócić kod błędu jeżeli:
- urządzenie, którego identyfikator EUI jest przesłany w żądaniu nie zostanie znalezione w bazie danych
- kod autoryzacyjny urządzenia przesłany w żądaniu nie jest zgodny z konfiguracją tego urządzenia w bazie danych.

Zobacz też: [Receiver API](/restapi/receiver.md)

## Przykład 1

Wysłanie nowych danych. Jeżeli jest oczekująca komenda dla tego urządzenia, to treść komendy będzie zwrócona w treści odpowiedzi.

### Przesłanie danych z odebraniem odpowiedzi

```shell
curl  -X POST \
  'cloud.localhost/api/receiver/io' \
  --header 'Content-Type: text/plain' \
  --header 'X-device-eui: DEVICE1' \
  --header 'Authorization: 0000018e7558c3e6' \
  --header 'X-data-separator: ;' \
  --data-raw 'temperature=15.0;humidity=23.2'
```

### Odpowiedź

W przypadku, gdy nie ma komend oczekujących na odebranie.

```shell
HTTP/1.1 200 OK
content-type: text/plain;charset=UTF-8
content-length: 0
```

### Odpowiedź

W przypadku, gdy jest komenda oczekująca na odebranie, jej treść będzie zawarta o odpowiedzi na zapytanie. Interpretacja treści komendy zależy od tego w jaki sposób ta komenda została wygenerowana.
Więcej o tym na stronie ....

```shell
HTTP/1.1 200 OK
content-type: text/plain;charset=UTF-8
content-length: 32

eyJ0eXBlIjoiYiIsInZhbHVlIjoxfQ==
```

<!-- TODO: zobacz też dokumentacja komend -->

### Odpowiedź 

```shell
```