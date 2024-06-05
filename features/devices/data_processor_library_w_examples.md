Oczywiście, poniżej znajduje się uzupełniona dokumentacja z dodanymi przykładami użycia dla każdej funkcji.

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

### Przykład użycia

<code>
const receivedData = [
    { name: "temperature", value: 22.5, timestamp: 1628765432 },
    { name: "humidity", value: 60, timestamp: 1628765432 }
];
const status = "ok";

sgx.verify(receivedData, status);
</code>

## `accept(name)`

Funkcja `accept` służy do zaakceptowania danych o podanej nazwie i zapisania ich w wynikach.

### Parametry

- `name` (String): Nazwa danych do zaakceptowania.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.accept("temperature");
```

## `addCommand(targetEUI, payload, overwrite)`

Funkcja `addCommand` służy do dodawania nowej komendy.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (Object): Dane w formacie JSON, które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy istniejąca komenda powinna zostać nadpisana.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
const targetEUI = "00124B0004F12345";
const payload = { command: "activate", parameters: { duration: 10 } };
const overwrite = true;

sgx.addCommand(targetEUI, payload, overwrite);
```

## `addPlainCommand(targetEUI, payload, overwrite)`

Funkcja `addPlainCommand` służy do dodawania nowej komendy w formacie zwykłego tekstu.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (Object): Dane w formacie JSON, które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy istniejąca komenda powinna zostać nadpisana.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
const targetEUI = "00124B0004F12345";
const payload = { command: "deactivate" };
const overwrite = false;

sgx.addPlainCommand(targetEUI, payload, overwrite);
```

## `addHexCommand(targetEUI, payload, overwrite)`

Funkcja `addHexCommand` służy do dodawania nowej komendy z ładunkiem w formacie szesnastkowym.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (String): Dane w formacie szesnastkowym, które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy istniejąca komenda powinna zostać nadpisana.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
const targetEUI = "00124B0004F12345";
const payload = "00FFAA01";
const overwrite = true;

sgx.addHexCommand(targetEUI, payload, overwrite);
```

## `addNotification(newType, newMessage)`

Funkcja `addNotification` służy do dodawania nowej notyfikacji.

### Parametry

- `newType` (String): Typ nowej notyfikacji.
- `newMessage` (String): Treść nowej notyfikacji.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.addNotification("info", "Device activated successfully.");
```

## `addVirtualData(newEUI, newName, newValue)`

Funkcja `addVirtualData` służy do dodawania nowych danych wirtualnych.

### Parametry

- `newEUI` (String): Unikalny identyfikator nowego urządzenia.
- `newName` (String): Nazwa nowych danych.
- `newValue` (Mixed): Wartość nowych danych.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.addVirtualData("00124B0004F67890", "virtualTemperature", 25);
```

## `getAverage(channelName, scope, newValue)`

Funkcja `getAverage` służy do uzyskiwania średniej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Średnia wartość dla danego kanału.

### Przykład użycia

```javascript
const average = sgx.getAverage("temperature", 10);
const newAverage = sgx.getAverage("temperature", 10, 23.

```markdown
);
```

## `getMinimum(channelName, scope, newValue)`

Funkcja `getMinimum` służy do uzyskiwania minimalnej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Minimalna wartość dla danego kanału.

### Przykład użycia

```javascript
const minimum = sgx.getMinimum("temperature", 10);
const newMinimum = sgx.getMinimum("temperature", 10, 18);
```

## `getMaximum(channelName, scope, newValue)`

Funkcja `getMaximum` służy do uzyskiwania maksymalnej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Maksymalna wartość dla danego kanału.

### Przykład użycia

```javascript
const maximum = sgx.getMaximum("temperature", 10);
const newMaximum = sgx.getMaximum("temperature", 10, 27);
```

## `getSum(channelName, scope, newValue)`

Funkcja `getSum` służy do uzyskiwania sumy wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Suma wartości dla danego kanału.

### Przykład użycia

```javascript
const sum = sgx.getSum("temperature", 10);
const newSum = sgx.getSum("temperature", 10, 22);
```

## `getLastValue(channelName)`

Funkcja `getLastValue` służy do uzyskiwania ostatniej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Mixed`: Ostatnia wartość dla danego kanału lub `null`, jeśli brak danych.

### Przykład użycia

```javascript
const lastValue = sgx.getLastValue("temperature");
```

## `getLastData(channelName)`

Funkcja `getLastData` służy do uzyskiwania ostatnich danych dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Object`: Ostatnie dane dla danego kanału.

### Przykład użycia

```javascript
const lastData = sgx.getLastData("temperature");
```

## `getModulo(value, divider)`

Funkcja `getModulo` służy do uzyskiwania reszty z dzielenia wartości przez dzielnik.

### Parametry

- `value` (Number): Wartość do podzielenia.
- `divider` (Number): Dzielnik.

### Zwraca

- `Number`: Reszta z dzielenia.

### Przykład użycia

```javascript
const modulo = sgx.getModulo(10, 3); // 1
```

## `getOutput()`

Funkcja `getOutput` służy do uzyskiwania wyników przetwarzania.

### Zwraca

- `Mixed`: Wynik przetwarzania.

### Przykład użycia

```javascript
const output = sgx.getOutput();
```

## `getTimestamp(channelName)`

Funkcja `getTimestamp` służy do uzyskiwania znacznika czasu dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Number`: Znacznik czasu dla danego kanału.

### Przykład użycia

```javascript
const timestamp = sgx.getTimestamp("temperature");
```

## `getTimestampUTC(y, m, d, h, min, s)`

Funkcja `getTimestampUTC` służy do uzyskiwania znacznika czasu UTC na podstawie podanych parametrów.

### Parametry

- `y` (Number): Rok.
- `m` (Number): Miesiąc.
- `d` (Number): Dzień.
- `h` (Number): Godzina.
- `min` (Number): Minuta.
- `s` (Number): Sekunda.

### Zwraca

- `Number`: Znacznik czasu UTC.

### Przykład użycia

```javascript
const timestampUTC = sgx.getTimestampUTC(2024, 6, 5, 12, 0, 0);
```

## `getValue(channelName)`

Funkcja `getValue` służy do uzyskiwania wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Mixed`: Wartość dla danego kanału lub `null`, jeśli brak danych.

### Przykład użycia

```javascript
const value = sgx.getValue("temperature");
```

## `getStringValue(channelName)`

Funkcja `getStringValue` służy do uzyskiwania wartości tekstowej dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `String`: Wartość tekstowa dla danego kanału lub `null`, jeśli brak danych.

### Przykład użycia

```javascript
const stringValue = sgx.getStringValue("temperature");
```

## `put(name, newValue, timestamp)`

Funkcja `put` służy do umieszczania nowych danych.

### Parametry

- `name` (String): Nazwa danych.
- `newValue` (Mixed): Nowa wartość danych.
- `timestamp` (Number, opcjonalnie): Znacznik czasu danych.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.put("temperature", 23.5);
sgx.put("temperature", 23.5, 1628765432);
```

## `setState(newState)`

Funkcja `setState` służy do ustawiania nowego stanu urządzenia.

### Parametry

- `newState` (String): Nowy stan urządzenia.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.setState("active");
```

## `setStatus(newStatus)`

Funkcja `setStatus` służy do ustawiania nowego statusu urządzenia.

### Parametry

- `newStatus` (String): Nowy status urządzenia.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.setStatus("offline");
```

## `reverseHex(hexStr)`

Funkcja `reverseHex` służy do odwracania kolejności znaków w łańcuchu szesnastkowym.

### Parametry

- `hexStr` (String): Łańcuch szesnastkowy.

### Zwraca

- `String`: Odwrócony łańcuch szesnastkowy.

### Przykład użycia

```javascript
const reversedHex = sgx.reverseHex("00FFAA01"); // "01AAFF00"
```

## `swap32(val)`

Funkcja `swap32` służy do zmiany kolejności bajtów w liczbie 32-bitowej.

### Parametry

- `val` (Number): Liczba 32-bitowa.

### Zwraca

- `Number`: Liczba z zmienioną kolejnością bajtów.

### Przykład użycia

```javascript
const swapped = sgx.swap32(0x12345678); // 0x78563412
```

## `distance(latitude1, longitude1, latitude2, longitude2)`

Funkcja `distance` służy do obliczania odległości między dwoma punktami geograficznymi.

### Parametry

- `latitude1` (Number): Szerokość geograficzna punktu 1.
- `longitude1` (Number): Długość geograficzna punktu 1.
- `latitude2` (Number): Szerokość geograficzna punktu 2.
- `longitude2` (Number): Długość geograficzna punktu 2.

### Zwraca

- `Number`: Odległość między dwoma punktami w kilometrach.

### Przykład użycia

```javascript
const dist = sgx.distance(52.2296756, 21.0122287, 41.8919300, 12.5113300);
```
