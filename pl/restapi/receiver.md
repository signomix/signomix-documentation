# Receiver API

## Spis Treści

- [Wprowadzenie](#wprowadzenie)
- [Adresy](#adresy)
  - [POST /api/receiver/io (JSON)](#post-receiverio-json)
  - [POST /api/receiver/io (Text)](#post-receiverio-text)
  - [POST /api/receiver/io (Form)](#post-receiverio-form)
  - [POST /api/receiver/in (JSON)](#post-receiverin-json)
  - [POST /api/receiver/in (Text)](#post-receiverin-text)
  - [POST /api/receiver/in (Form)](#post-receiverin-form)
  - [POST /api/receiver/bulk](#post-receiverbulk)
  - [POST /api/receiver/ttn3/up](#post-receiverttn3)
  - [POST /api/receiver/chirpstack](#post-receiverchirpstack)
- [Przykłady Użycia](#przyklady-uzycia)

## <a name="wprowadzenie"></a>Wprowadzenie

Niniejsza dokumentacja opisuje REST API dla odbiornika danych IoT. API umożliwia przesyłanie danych w formatach JSON, tekstowym oraz jako formularze, a także umożliwia przesyłanie danych w trybie wsadowym (bulk).

Zobacz też: [Przesyłanie danych](sending-data.md)

## Dokumentacja REST API Generic

### <a name="adresy"></a>Adresy

#### <a name="post-receiverio-json"></a>POST /api/receiver/io (JSON)

Przetwarza dane w formacie JSON.

**URL**: `/api/receiver/io`

**Metoda HTTP**: `POST`

**Nagłówki**:
- `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)
- `X-device-eui`: EUI urządzenia (opcjonalny w zależności od konfiguracji)

**Treść żądania**:
```json
{
    "dev_eui": "string",
    "gateway_eui": "string",
    "timestamp": "long",
    "clientname": "string",
    "payload": "string",
    "hex_payload": "string",
    "payload_fields": [
        {
            "name": "string",
            "value": "string"
        }
    ]
}
```

**Treść odpowiedzi**:
- `200 OK` – Sukces
- `401 Unauthorized` – Brak nagłówka autoryzacyjnego
- `404 Not Found` – Urządzenie nieznane lub nieaktywne
- `400 Bad Request` – Błąd w przetwarzaniu danych

#### <a name="post-receiverio-text"></a>POST /api/receiver/io (Text)

Przetwarza dane w formacie tekstowym.

**URL**: `/api/receiver/io`

**Metoda HTTP**: `POST`

**Nagłówki**:
- `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)
- `X-device-eui`: EUI urządzenia (opcjonalny w zależności od konfiguracji)
- `X-data-separator`: Separator danych (opcjonalny)

**Treść żądania**: Tekst

**Treść odpowiedzi**:
- `200 OK` – Sukces
- `401 Unauthorized` – Brak nagłówka autoryzacyjnego
- `404 Not Found` – Urządzenie nieznane lub nieaktywne
- `400 Bad Request` – Błąd w przetwarzaniu danych

#### <a name="post-receiverio-form"></a>POST /api/receiver/io (Form)

Przetwarza dane przesłane jako formularz.

**URL**: `/api/receiver/io`

**Metoda HTTP**: `POST`

**Nagłówki**:
- `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)
- `X-device-eui`: EUI urządzenia (opcjonalny w zależności od konfiguracji)

**Treść żądania**: Formularz URL-encoded

**Treść odpowiedzi**:
- `200 OK` – Sukces
- `401 Unauthorized` – Brak nagłówka autoryzacyjnego
- `404 Not Found` – Urządzenie nieznane lub nieaktywne
- `400 Bad Request` – Błąd w przetwarzaniu danych

#### <a name="post-receiverin-json"></a>POST /api/receiver/in (JSON)

Przetwarza dane w formacie JSON.

**URL**: `/api/receiver/in`

**Metoda HTTP**: `POST`

**Nagłówki**:
- `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)
- `X-device-eui`: EUI urządzenia (opcjonalny w zależności od konfiguracji)

**Treść żądania**:
```json
{
    "dev_eui": "string",
    "gateway_eui": "string",
    "timestamp": "long",
    "clientname": "string",
    "payload": "string",
    "hex_payload": "string",
    "payload_fields": [
        {
            "name": "string",
            "value": "string"
        }
    ]
}
```

**Treść odpowiedzi**:
- `200 OK` – Sukces
- `401 Unauthorized` – Brak nagłówka autoryzacyjnego
- `404 Not Found` – Urządzenie nieznane lub nieaktywne
- `400 Bad Request` – Błąd w przetwarzaniu danych

#### <a name="post-receiverin-text"></a>POST /api/receiver/in (Text)

Przetwarza dane w formacie tekstowym.

**URL**: `/api/receiver/in`

**Metoda HTTP**: `POST`

**Nagłówki**:
- `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)
- `X-device-eui`: EUI urządzenia (opcjonalny w zależności od konfiguracji)
- `X-data-separator`: Separator danych (opcjonalny)

**Treść żądania**: Tekst

**Treść odpowiedzi**:
- `200 OK` – Sukces
- `401 Unauthorized` – Brak nagłówka autoryzacyjnego
- `404 Not Found` – Urządzenie nieznane lub nieaktywne
- `400 Bad Request` – Błąd w przetwarzaniu danych

#### <a name="post-receiverin-form"></a>POST /api/receiver/in (Form)

Przetwarza dane przesłane jako formularz.

**URL**: `/api/receiver/in`

**Metoda HTTP**: `POST`

**Nagłówki**:
- `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)
- `X-device-eui`: EUI urządzenia (opcjonalny w zależności od konfiguracji)

**Treść żądania**: Formularz URL-encoded

**Treść odpowiedzi**:
- `200 OK` – Sukces
- `401 Unauthorized` – Brak nagłówka autoryzacyjnego
- `404 Not Found` – Urządzenie nieznane lub nieaktywne
- `400 Bad Request` – Błąd w przetwarzaniu danych

#### <a name="post-receiverbulk"></a>POST /api/receiver/bulk

Przetwarza wsadowe przesyłanie danych w formacie CSV.

**URL**: `/api/receiver/bulk`

**Metoda HTTP**: `POST`

**Nagłówki**:
- `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)
- `X-device-eui`: EUI urządzenia

**Treść żądania**: Dane multipart/form-data

**Treść odpowiedzi**:
- `200 OK` – Sukces
- `401 Unauthorized` – Brak nagłówka autoryzacyjnego
- `404 Not Found` – Urządzenie nieznane lub nieaktywne
- `400 Bad Request` – Błąd w przetwarzaniu danych

## Dokumentacja REST API TTN

The `ReceiverResourceTtn` class provides REST API endpoints for receiving and processing IoT data from The Things Network (TTN). This API supports options and POST requests for handling data and authorization.

### Adresy

#### <a name="post-receiverttn3"></a>POST /api/receiver/ttn3/up

Receives IoT data in JSON format, decodes it, transforms it into an internal format, and processes it. If authorization is required, the request must include an Authorization header.

**URL** `/api/receiver/ttn3/up`

**Metoda** `POST`

**Nagłówki żądania**
  - `Authorization` (optional if `device.authorization.required` is `false`): Authorization token.

**Treść żadania** - `application/json`

**Wynik** `text/plain`

**Odpowiedzi**

- Status: `200 OK`
  - Body: `"OK"` if data processing is successful.
- Status: `400 Bad Request`
  - Body: `"error while reading the data"` if the data cannot be read.
- Status: `401 Unauthorized`
  - Body: `"no authorization header found"` if authorization is required but the header is missing or blank.
- Status: `500 Internal Server Error`
  - Body: `"error while processing the data"` if an error occurs during data processing.


## Dokumentacja REST API Chirpstack

### Adresy

#### <a name="post-receiverchirpstack"></a>POST /api/receiver/chirpstack

**URL**: `/api/receiver/chirpstack`

**Metoda HTTP**: `POST`

**Nagłówki**
  - `Authorization`: Klucz autoryzacyjny (opcjonalny w zależności od konfiguracji)

**Parametry zapytania**
  - `event`: (Required) Specifies the type of event. Supported values are `up` and `join`.

**Treść żądania**
  - The body should contain the event data in JSON format.

**Kod odpowiedzi**

- `200 OK` - Indicates that the request was successfully processed.
- `400 Bad Request`<br>
    Returned if the `event` parameter is missing or if there is an error while reading the data.<br>
    Example response: `{"message": "event parameter missing"}`
- `401 Unauthorized`<br>
    Returned if authorization is required and the `Authorization` header is missing or blank.<br>
    Example response: `{"message": "no authorization header found"}`
- `500 Internal Server Error`- Returned if there is an error while processing the data.


## <a name="przyklady_uzycia"></a>Przykłady Użycia

### Rest API Generic

#### Przykład 1: Przesyłanie danych w formacie JSON

**Żądanie**:
```bash
curl -X POST "http://example.com/api/receiver/io" \
    -H "Authorization: 0102030405" \
    -H "X-device-eui: ABC123" \
    -H "Content-Type: application/json" \
    -d '{
        "dev_eui": "ABC123",
        "timestamp": 1627890123,
        "clientname": "ExampleClient",
        "payload": "example_payload",
        "hex_payload": "6865785f7061796c6f6164",
        "payload_fields": [
            {"name": "temperature", "value": "22.5"},
            {"name": "humidity", "value": "60"}
        ]
    }'
```

**Odpowiedź**:
```
200 OK
```

#### Przykład 2: Przesyłanie danych w formacie tekstowym

**Żądanie**:
```bash
curl -X POST "http://example.com/api/receiver/io" \
    -H "Authorization: 0102030405" \
    -H "X-device-eui: ABC123" \
    -H "X-data-separator: ;" \
    -H "Content-Type: text/plain" \
    -d "temperature=22.5;humidity=60"
```

**Odpowiedź**:
```
200 OK
```

#### Przykład 3: Przesyłanie danych jako formularz

**Żądanie**:
```bash
curl -X POST "http://example.com/api/receiver/io" \
    -H "Authorization: 0102030405" \
    -H "X-device-eui: ABC123" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "temperature=22.5&humidity=60"
```

**Odpowiedź**:

```
200 OK
```

#### Przykład 4: Przesyłanie danych wsadowych

**Żądanie**:
```bash
curl -X POST "http://example.com/api/receiver/bulk" \
    -H "Authorization: 0102030405" \
    -H "X-device-eui: ABC123" \
    -F "file=@data.csv"
```

**Odpowiedź**:
```
200 OK
```

**Przykładowa zawartość `data.csv`**:
```csv
dev_eui,gateway_eui,timestamp,clientname,payload,hex_payload,payload_fields
ABC123,DEF456,1627890123,ExampleClient,example_payload,6865785f7061796c6f6164,"[{""name"": ""temperature"", ""value"": ""22.5""}, {""name"": ""humidity"", ""value"": ""60""}]"
```

### Rest API TTN

#### Przykład 1

**Żądanie**
```bash
curl -X POST `http://example.com/api/receiver/ttn3/up` \
    -H `Authorization: 0102030405` \
    -H `Content-Type: application/json` \
    -d '{
        "deviceEui": "0004A30B002C3A9D",
        "timestamp": 1627382993,
        "payloadFields": {
            "temperature": 23.5,
            "humidity": 56
        }
    }
```

**Odpowiedź**
```
OK
```
