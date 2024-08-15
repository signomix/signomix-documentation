# Data Query Language (DQL)

Signomix udostępnia język zapytań o dane (DQL), umożliwiający użytkownikowi serwisu definiowanie rodzaju i zakresu danych prezentowanych przez kontrolki pulpitu oraz pobieranych za pomocą API.

Wyrażenie DQL składa się z warunków oraz ich parametrów.

Ogólnie wyrażenie DQL ma 2 możliwe formy:
1. Pobranie danych odbieranych od urządzenia
```
[GET] {definicja zakresu danych} [BY {specyfikacja raportu}] [[WHERE] {definicja wyboru}] [[AS] {definicja formatu}] 
```
2. Pobranie danych zapisywanych przez urządzenie wirtualne. Stosowane w specyficznych przypadkach, zostanie omówione w odrębnym dokumencie.
```
[GET] virtual
```
Przy czym:
- słowa kluczowe `GET`, `WHERE`, `AS` mają jedynie znaczenie informacyjne i mogą być pominięte,
- wielkość liter nie ma znaczenia.

## Definicja zakresu danych
- `last n` - pobranie n ostatnich wartości określonej danej
- `average n [new v]` - pobranie średniej wartości wyliczonej z `n` ostatnich pomiarów, opcjonalnie uwzględniając dodatkową wartość `v`
- `minimum n [new v]` - pobranie minimalnej wartości z `n` ostatnich pomiarów, opcjonalnie uwzględniając dodatkową wartość `v`
- `maximum n [new v]` - pobranie maksymalnej wartości z `n` ostatnich pomiarów, opcjonalnie uwzględniając dodatkową wartość `v`
- `from {d1} [to {d2}]` - od punktu czasowego zdefiniowanego przez `{d1}`, do punktu czasowego zdefiniowanego przez `{d1}`.
- `sback n` - uwzględnienie danych zarejestrowanych maksymalnie `n` sekund wcześniej
- `ascending` - sortuj wynik zgodnie z rosnącą datą pomiaru
- `descending` - sortuj wynik zgodnie z malejącą datą pomiaru

Parametr `sback` jest uwzględniany przy pobieraniu ostatnich pomiarów grupy. Jeśli nie jest podany, to uwzględniane są dane zarejestrowane maksymalnie godzinę wcześniej. Parametr ten umożliwia odrzucenie danych ze źródeł, które nie przesłały danych w ostatnim czasie (np. przestały działać, ale istnieją dane historyczne, które nie powinny być prezentowane w raporcie).

Definicja punktów czasowych `{d1, d2}`:
- data zapisana w formacie `yyyy-MM-dd'T'HH:mm:ss.SSSX` lub `yyyy-MM-dd'T'HH:mm:ssX` lub jako `Unix time`  (https://en.wikipedia.org/wiki/Unix_time) (może być podana również jako liczba milisekund)
- `-Xd` - X dób wstecz od chwili bieżącej - TO NIE DZIAŁA
- `-0d-StrefaCzasowa` - od początku bieżącej doby w podanej strefie czasowej
- `-0d-UTC` od początku doby w strefie UTC
- `-0M-StrefaCzasowa` od początku bieżącego miesiąca w podanej strefie czasowej
- `-0M-UTC` od początku bieżącego miesiąca w strefie UTC
- `-Xh` - X godzin wstecz od chwili bieżącej
- `-Xm` - X minut wstecz od chwili bieżącej

Przykłady:
```
get last 10
last 10
from -2h to -1h
from 2023-03-10T00:00:00Z to 2023-03-10T12:00:00Z
from 2023-03-23T00:05:00~01:00 to 2023-03-23T00:07:00~01:00
from 1679363129 to 1679395529
from -0M-Europe_Warsaw
from -0M-UTC
from -0d-Europe/Warsaw to -0m
```

## Specyfikacja raportu

- `report className` - nazwa klasy Java implementującej logikę raportu (patrz: [Server Raportów](/features/reports/index.md))

## Definicja wyboru

- `project nazwa` - pobranie danych otagowanych nazwą projektu równą `nazwa`
- `status n` - pobranie danych dla których urządzenie miało status o wartości równej `n`
- `eui identyfikator` - pobranie danych dotyczących urządzenia o identyfikatorze `identyfikator`
- `group identyfikator` - pobranie danych dotyczących urządzeń należących do grupy o identyfikatorze `identyfikator`
- `channel definicja` - pobranie pomiarów o nazwach zawartych w polu `definicja` - nazwy oddzielone przecinkami lub znak `*` oznaczający wszystkie nazwy pomiarów dla danego źródła


Przykłady:
```
last 10 project test
last 10 status 1
last 10 project test status 1
last 3 eui 010203040506 channel *
last 3 eui 010203040506 channel temperature,humidity
```

## Definicja formatu
> Uwaga: Definicja formatu ma zastosowanie jedynie w przypadku pobierania danych urządzenia za pomocą API `/api/iot/device/{eui}?{query}`. Nie jest uwzględniana przez kontrolki pulpitu.

- `timeseries` - zastosowanie uproszczonego formatu JSON
- `csv.timeseries` - dane w formacie CSV

Przykład danych zwracanych w wyniku zapytania bez definicji formatu:
```
last 2

[
  [
    {
      "deviceEUI":"020305",
      "name":"temperature",
      "value":30.0,
      "timestamp":1679526300000,
      "stringValue":null
    },
    {
      "deviceEUI":"020305",
      "name":"temperature",
      "value":30.0,
      "timestamp":1679526411476,
      "stringValue":null
    }
  ]
]
```

Przykład uproszczonego formatu JSON:
```
last 2 timeseries
get last 2 as timeseries

[
  [
    [
      "timestamp",
      "temperature",
      "humidity"
    ],
    [
      1679526411476,
      30.0,
      46.0
    ],
    [
      1679526300000,
      30.0,
      46.0
    ]
  ]
]
```
Przykład formatu CSV:
```
last 2 csv.timeseries

timestamp,temperature,humidity
1679526411476,30.0,46.0
1679526300000,30.0,46.0
```

