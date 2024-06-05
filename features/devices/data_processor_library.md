Oto kompletna dokumentacja techniczna dla podanej biblioteki, sformatowana jako Markdown z uwzględnieniem wszystkich funkcji i dodanym spisem treści. Symbol `sgx0` został zastąpiony przez `sgx`.

```markdown
## Spis treści

- [verify](#verifyreceived-receivedstatus)
- [accept](#acceptname)
- [addCommand](#addcommandtargeteui-payload-overwrite)
- [addPlainCommand](#addplaincommandtargeteui-payload-overwrite)
- [addHexCommand](#addhexcommandtargeteui-payload-overwrite)
- [addNotification](#addnotificationnewtype-newmessage)
- [addVirtualData](#addvirtualdataneweui-newname-newvalue)
- [getAverage](#getaveragechannelname-scope-newvalue)
- [getMinimum](#getminimumchannelname-scope-newvalue)
- [getMaximum](#getmaximumchannelname-scope-newvalue)
- [getSum](#getsumchannelname-scope-newvalue)
- [getLastValue](#getlastvaluechannelname)
- [getLastData](#getlastdatachannelname)
- [getModulo](#getmodulovalue-divider)
- [getOutput](#getoutput)
- [getTimestamp](#gettimestampchannelname)
- [getTimestampUTC](#gettimestamputcy-m-d-h-min-s)
- [getValue](#getvaluechannelname)
- [getStringValue](#getstringvaluechannelname)
- [put](#putname-newvalue-timestamp)
- [setState](#setstatenewstate)
- [setStatus](#setstatusnewstatus)
- [reverseHex](#reversehexhexstr)
- [swap32](#swap32val)
- [distance](#distancelatitude1-longitude1-latitude2-longitude2)

## `verify(received, receivedStatus)`

Funkcja `verify` służy do weryfikacji otrzymanych danych i aktualizacji stanu obiektu.

### Parametry

- `received` (Array): Tablica obiektów danych do weryfikacji.
- `receivedStatus` (String): Status otrzymanych danych.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `accept(name)`

Funkcja `accept` służy do zaakceptowania danych o podanej nazwie i zapisania ich w wynikach.

### Parametry

- `name` (String): Nazwa danych do zaakceptowania.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `addCommand(targetEUI, payload, overwrite)`

Funkcja `addCommand` służy do dodawania nowej komendy.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (Object): Dane w formacie JSON, które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy istniejąca komenda powinna zostać nadpisana.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `addPlainCommand(targetEUI, payload, overwrite)`

Funkcja `addPlainCommand` służy do dodawania nowej komendy w formacie zwykłego tekstu.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (Object): Dane w formacie JSON, które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy istniejąca komenda powinna zostać nadpisana.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `addHexCommand(targetEUI, payload, overwrite)`

Funkcja `addHexCommand` służy do dodawania nowej komendy z ładunkiem w formacie szesnastkowym.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (String): Dane w formacie szesnastkowym, które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy istniejąca komenda powinna zostać nadpisana.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `addNotification(newType, newMessage)`

Funkcja `addNotification` służy do dodawania nowej notyfikacji.

### Parametry

- `newType` (String): Typ nowej notyfikacji.
- `newMessage` (String): Treść nowej notyfikacji.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `addVirtualData(newEUI, newName, newValue)`

Funkcja `addVirtualData` służy do dodawania nowych danych wirtualnych.

### Parametry

- `newEUI` (String): Unikalny identyfikator nowego urządzenia.
- `newName` (String): Nazwa nowych danych.
- `newValue` (Mixed): Wartość nowych danych.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `getAverage(channelName, scope, newValue)`

Funkcja `getAverage` służy do uzyskiwania średniej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Średnia wartość dla danego kanału.

## `getMinimum(channelName, scope, newValue)`

Funkcja `getMinimum` służy do uzyskiwania minimalnej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Minimalna wartość dla danego kanału.

## `getMaximum(channelName, scope, newValue)`

Funkcja `getMaximum` służy do uzyskiwania maksymalnej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Maksymalna wartość dla danego kanału.

## `getSum(channelName, scope, newValue)`

Funkcja `getSum` służy do uzyskiwania sumy wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Suma wartości dla danego kanału.

## `getLastValue(channelName)`

Funkcja `getLastValue` służy do uzyskiwania ostatniej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Mixed`: Ostatnia wartość dla danego kanału lub `null`, jeśli brak danych.

## `getLastData(channelName)`

Funkcja `getLastData` służy do uzyskiwania ostatnich danych dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Object`: Ostatnie dane dla danego kanału.

## `getModulo(value, divider)`

Funkcja `getModulo` służy do obliczania reszty z dzielenia.

### Parametry

- `value` (Number): Wartość do podzielenia.
- `divider` (Number): Dzielnik.

### Zwraca

- `Number`: Reszta z dzielenia `value` przez `divider`.

## `getOutput()`

Funkcja `getOutput` służy do uzyskiwania wyniku operacji.

### Zwraca

- `Mixed`: Wynik operacji.

## `getTimestamp(channelName)`

Funkcja `getTimestamp` służy do uzyskiwania znacznika czasu dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Number`: Znacznik czasu dla danego kanału.

## `getTimestampUTC(y, m, d, h, min, s)`

Funkcja `getTimestampUTC` służy do uzyskiwania znacznika czasu UTC.

### Parametry

- `y` (Number): Rok.
- `m` (Number): Miesiąc.
- `d` (Number

): Dzień.
- `h` (Number): Godzina.
- `min` (Number): Minuta.
- `s` (Number): Sekunda.

### Zwraca

- `Number`: Znacznik czasu UTC.

## `getValue(channelName)`

Funkcja `getValue` służy do uzyskiwania wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Mixed`: Wartość dla danego kanału lub `null`, jeśli brak danych.

## `getStringValue(channelName)`

Funkcja `getStringValue` służy do uzyskiwania wartości tekstowej dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `String`: Wartość tekstowa dla danego kanału lub `null`, jeśli brak danych.

## `put(name, newValue, timestamp)`

Funkcja `put` służy do umieszczania nowych danych.

### Parametry

- `name` (String): Nazwa danych.
- `newValue` (Mixed): Nowa wartość danych.
- `timestamp` (Number, opcjonalnie): Znacznik czasu danych.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `setState(newState)`

Funkcja `setState` służy do ustawiania nowego stanu urządzenia.

### Parametry

- `newState` (String): Nowy stan urządzenia.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `setStatus(newStatus)`

Funkcja `setStatus` służy do ustawiania nowego statusu urządzenia.

### Parametry

- `newStatus` (String): Nowy status urządzenia.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

## `reverseHex(hexStr)`

Funkcja `reverseHex` służy do odwracania kolejności znaków w łańcuchu szesnastkowym.

### Parametry

- `hexStr` (String): Łańcuch szesnastkowy.

### Zwraca

- `String`: Odwrócony łańcuch szesnastkowy.

## `swap32(val)`

Funkcja `swap32` służy do zmiany kolejności bajtów w liczbie 32-bitowej.

### Parametry

- `val` (Number): Liczba 32-bitowa.

### Zwraca

- `Number`: Liczba z zmienioną kolejnością bajtów.

## `distance(latitude1, longitude1, latitude2, longitude2)`

Funkcja `distance` służy do obliczania odległości między dwoma punktami geograficznymi.

### Parametry

- `latitude1` (Number): Szerokość geograficzna punktu 1.
- `longitude1` (Number): Długość geograficzna punktu 1.
- `latitude2` (Number): Szerokość geograficzna punktu 2.
- `longitude2` (Number): Długość geograficzna punktu 2.

### Zwraca

- `Number`: Odległość między dwoma punktami w kilometrach.

```
