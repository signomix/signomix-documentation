# Język Zapytania Danych (DQL)

Signomix oferuje Język Zapytania Danych (DQL), który pozwala użytkownikom definiować, jakie dane mają być wyświetlane na pulpitach oraz pobierane przez API.

## Budowa Zapytania DQL

Zapytania DQL składają się z warunków i ich parametrów. Można je wyrażać na dwa sposoby:

1. **Pobranie danych z urządzenia**
`[USING] [{Secyfikacja Raportu}] [GET] {Zakres Danych} [[WHERE] {Wybór Danych}] [[AS] {Format Danych Wyjściowych}]`

2. **Pobranie danych z urządzenia wirtualnego** 
`[GET] virtual`

>**Uwagi**<br>
>- Słowa kluczowe takie jak `GET`, `WHERE`, `AS`, `USING` są opcjonalne i mogą być pominięte.
>- Wielkość liter nie ma znaczenia.


## Specyfikacja Raportu

Składnia: `report className`

- `report` - wymagane słowo kluczowe
- `className` - nazwa klasy Java implementującej logikę raportu.

## Zakres Danych

Składnia: `[last n | average n [new v]| minimum n [new v] | maximum n [new v] | from d1 [to d2]] [sback n] [ascending|descending]

- `last n` - pobierz n ostatnich wartości
- `average n [new v]` - średnia z n ostatnich pomiarów, z opcjonalną wartością `v`
- `minimum n [new v]` - minimalna wartość z n ostatnich pomiarów, z opcjonalną wartością `v`
- `maximum n [new v]` - maksymalna wartość z n ostatnich pomiarów, z opcjonalną wartością `v`
- `from t1 [to t2]` - dane od punktu czasowego `t1` do `t2`
- `sback n` - uwzględnij dane sprzed maksymalnie `n` sekund
- `ascending` - sortuj wyniki według rosnącej daty
- `descending` - sortuj wyniki według malejącej daty

> Parametr `sback` pozwala odrzucić dane z urządzeń, które nie przesłały informacji w ostatnim czasie, co może być przydatne, gdy chcemy wykluczyć nieaktualne źródła danych.

Punkty czasowe `t1 i t2` mogą być określane w różnych formatach, w tym:
- `yyyy-MM-dd'T'HH:mm:ss.SSSX` (ISO 8601)
- `Unix time` (czas w sekundach od 1970-01-01)
- `-Xd`, `-0d-StrefaCzasowa`, `-0d-UTC` i inne

Przykład:

```
get last 10 from -2h to -1h from 2023-03-10T00:00:00Z to 2023-03-10T12:00:00Z
```

## Wybór Danych

Składnia: `eui|group identyfikator channel definicja `

- `project nazwa` - dane otagowane nazwą projektu
- `status n` - dane o statusie równym `n`
- `eui identyfikator` - dane pozyskane z urządzenia o identyfikatorze `identyfikator`
- `group identyfikator` - dane pozyskane z grupy o identyfikatorze `identyfikator`
- `channel definicja` - dane pomiarów według nazw podanych w `definicja` (nazwy oddzielone przecinkami, bez spacji)

Przykład:

`last 10 eui 010203040506 channel temperature,humidity project test `


## Format Danych Wyjściowych

> **Uwaga**<br>
>Znaczenie tego parametru może się zmienić. Nie zalecam jego użycia bez konsultacji.

Wszystkie raporty zwracają dane w formacie JSON. W przypadku API `/api/iot/device/{eui}?{query}` można również zdefiniować format zwracanych danych jako:

- `timeseries` - uproszczony format JSON
- `csv.timeseries` - format CSV

### Przykład JSON

last 2

```
[ 
    [ { "deviceEUI":"020305", "name":"temperature", "value":30.0, "timestamp":1679526300000 },
     ... 
     ] 
]
```
last 2 csv.timeseries

```
timestamp,temperature,humidity 
1679526411476,30.0,46.0
```