# Data Query Language (DQL)

Signomix udostępnia język zapytań o dane (DQL), umożliwiający użytkownikowi serwisu definiowanie rodzaju i zakresu danych prezentowanych przez kontrolki pulpitu oraz pobieranych za pomocą API.

Wyrażenie DQL składa się z warunków oraz ich parametrów.

Ogólnie wyrażenie DQL ma 2 możliwe formy:
1. Pobranie danych odbieranych od urządzenia
```
[USING] {specyfikacja raportu} [WHERE] {definicja wyboru} [GET] {definicja zakresu danych} [{definicja operacji}] [[AS] {definicja formatu}]
```
2. Pobranie danych zapisywanych przez urządzenie wirtualne. Stosowane w specyficznych przypadkach, zostanie omówione w odrębnym dokumencie.
```
[GET] virtual
```

Przy czym:
- słowa kluczowe `USING`, `GET`, `WHERE`, `AS` mają jedynie znaczenie informacyjne i mogą być pominięte,
- wielkość liter nie ma znaczenia.

## Specyfikacja raportu

- `report className` - gdzie `className` to nazwa klasy Java implementującej logikę raportu (patrz: [Server Raportów](/features/reports/index.md))
- `class className` - to samo co `report className`

## Definicja wyboru

- `project nazwa` - pobranie danych otagowanych nazwą projektu równą `nazwa`
- `status n` - pobranie danych dla których urządzenie miało status o wartości równej `n`
- `eui identyfikator` - pobranie danych dotyczących urządzenia o identyfikatorze `identyfikator`
- `group identyfikator` - pobranie danych dotyczących urządzeń należących do grupy o identyfikatorze `identyfikator`
- `channel definicja` - pobranie pomiarów o nazwach zawartych w polu `definicja` - nazwy oddzielone przecinkami lub znak `*` oznaczający wszystkie nazwy pomiarów dla danego źródła
- `notnull` - odrzuć rekordy (pomiary z tym samym znacznikiem czasu), które nie mają kompletu wartości (patrz: `channel definicja`)
- `deltas` - pobierz przyrosty wartości pomiarów

Przykłady:
```
project test
status 1
project test status 1
eui 010203040506 channel *
eui 010203040506 channel temperature,humidity
```

## Definicja zakresu danych
- `limit n` - pobranie n ostatnich wartości określonej danej
- `average n [new v]` - pobranie średniej wartości wyliczonej z `n` ostatnich pomiarów, opcjonalnie uwzględniając dodatkową wartość `v`
- `minimum n [new v]` - pobranie minimalnej wartości z `n` ostatnich pomiarów, opcjonalnie uwzględniając dodatkową wartość `v`
- `maximum n [new v]` - pobranie maksymalnej wartości z `n` ostatnich pomiarów, opcjonalnie uwzględniając dodatkową wartość `v`
- `from {d1} [to {d2}]` - od punktu czasowego zdefiniowanego przez `{d1}`, do punktu czasowego zdefiniowanego przez `{d1}`.
- `sback n` - uwzględnienie danych zarejestrowanych maksymalnie `n` sekund wcześniej
- `ascending` - sortuj wynik zgodnie z rosnącą datą pomiaru
- `descending` - sortuj wynik zgodnie z malejącą datą pomiaru
- `deltas` - pobierz przyrosty wartości pomiarów
- `interval n intervalName` - pobierz dane dla `n` ostatnich przedziałów czasowych o nazwie `intervalName`
- `zone strefaCzasowa` - uwzględnij strefę czasową `strefaCzasowa` przy określaniu punktów czasowych (np. `Europe/Warsaw`, `UTC`). Domyślnie używana jest strefa czasowa `UTC`.
- `gapfill` - wypełnij luki w danych pomiarowych, które nie mają wartości dla danego przedziału czasowego. W przypadku braku wartości pomiaru, zostanie zwrócona wartość zarejestrowana w poprzednim przedziale czasowym. 
- 
Nazwy przedziałów czasowych `intervalName` są zdefiniowane w konfiguracji serwera Signomix. Domyślnie dostępne są:
- `second` - przedział czasowy o długości 1 sekundy
- `minute` - przedział czasowy o długości 1 minuty
- `hour` - przedział czasowy o długości 1 godziny
- `day` - przedział czasowy o długości 1 dnia
- `week` - przedział czasowy o długości 1 tygodnia
- `month` - przedział czasowy o długości 1 miesiąca
- `quarter` - przedział czasowy o długości 3 miesięcy
- `year` - przedział czasowy o długości 1 roku

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

## Definicja operacji

Wybrane raporty mogą wspierać dodatkowe operacje, które są wykonywane na danych przed ich zwróceniem. Operacje te są definiowane w specyfikacji raportu i mogą być różne dla różnych raportów. W przypadku raportu `IntervalReport` dostępna jest operacja pomnożenia wartości pomiarów przez wartość pobraną z innego źródła.

- `mpy` - nazwa mnożnika - pomiaru, przez który mają być pomnożone wartości pomiarów zwróconych przez raport
- `mpyeui` - identyfikator urządzenia, z którego ma być pobrana wartość mnożnika

Przykład: pobranie przyrostów wartości (co 30 dni) pomiaru `counter` z urządzenia `WATERMETTER` i pomnożenia  ich przez wartość pomiaru `water` (cena 1m3 wody) zapisanego w źródle danych `PRICES`:
```
report IntervalReport eui WATERMETTER channel counter interval 30 day mpy water mpyEui PRICES
```


## Definicja formatu

Domyślnym formatem danych jest JSON. Dla wybranych raportów możliwe jest również pobranie danych w formacie CSV lub HTML. W takim przypadku można wybrać format danych poprzez dodanie słowa kluczowego `format` i nazwy formatu do wyrażenia DQL.

- `format json` - dane w formacie JSON (domyślny)
- `format csv` - dane w formacie CSV
- `format html` - dane w formacie HTML


