## Spis treści

Definicja źródła danych (urządzenia) w Signomiksie umożliwia zdefiniowanie kodu dla procesora danych. W momencie odebrania nowych danych z tego źródła, procesor danych uruchamia interpreter języka JavaScript i wykonuje kod zdefiniowany dla tego źródła danych.

Tworząc kod dla procesora użytkownik może wykorzystać funkcje biblioteki `sgx` wbudowanej w procesor danych. Poniżej dokumentacja tej biblioteki.

<!-- TODO zmienne biblioteki -->

- [verify](#verify)
- [accept](#accept)
- [addCommand](#addcommand)
- [addPlainCommand](#addplaincommand)
- [addHexCommand](#addhexcommand)
- [addNotification](#addnotification)
- [addVirtualData](#addvirtualdata)
- [getAverage](#getaverage)
- [getMinimum](#getminimum)
- [getMaximum](#getmaximum)
- [getSum](#getsum)
- [getLastValue](#getlastvalue)
- [getLastData](#getlastdata)
- [getModulo](#getmodulo)
- [getOutput](#getoutput)
- [getTimestamp](#gettimestamp)
- [getTimestampUTC](#gettimestamputc)
- [getValue](#getvalue)
- [getStringValue](#getstringvalue)
- [put](#put)
- [setState](#setstate)
- [setStatus](#setstatus)
- [reverseHex](#reversehex)
- [swap32](#swap32)
- [distance](#distance)
- [homeDistance](#homeDistance)

## <a name="verify"></a>`verify(received, receivedStatus)`

Funkcja `verify` służy do weryfikacji otrzymanych danych i aktualizacji stanu obiektu.

### Parametry

- `received` (Array): Tablica obiektów danych do weryfikacji.
- `receivedStatus` (String): Status otrzymanych danych.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
var receivedData = [
    { name: "temperature", value: 22.5, timestamp: 1628765432 },
    { name: "humidity", value: 60, timestamp: 1628765432 }
];
var status = "ok";

sgx.verify(receivedData, status);
```

## <a name="accept"></a>`accept(name)`

Funkcja `accept` służy do zaakceptowania danych o podanej nazwie i zapisania ich w wynikach. Jej wywołanie może być konieczne w przypadku użycia w kodzie funkcji `put`.

Patrz też: [put](#put)

### Parametry

- `name` (String): Nazwa danych do zaakceptowania.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.accept("temperature");
```

## <a name="addcommand"></a>`addCommand(targetEUI, payload, overwrite)`

Funkcja `addCommand` służy do dodawania nowej komendy.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (Object): Dane (obiekt JavaScript), które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy unieważnić wcześniejsze (jeszcze nie przekazane) komendy..

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
var targetEUI = "00124B0004F12345";
var payload = { command: "activate", parameters: { duration: 10 } };
var overwrite = true;

sgx.addCommand(targetEUI, payload, overwrite);
```

## <a name="addplaincommand"></a>`addPlainCommand(targetEUI, payload, overwrite)`

Funkcja `addPlainCommand` służy do dodawania nowej komendy w formacie zwykłego tekstu.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (String): Tekst, który ma być wysłany jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy unieważnić wcześniejsze (jeszcze nie przekazane) komendy..

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
var targetEUI = "00124B0004F12345";
var payload = 'start'
var overwrite = false;

sgx.addPlainCommand(targetEUI, payload, overwrite);
```

## <a name="addhexcommand"></a>`addHexCommand(targetEUI, payload, overwrite)`

Funkcja `addHexCommand` służy do dodawania nowej komendy z ładunkiem w formacie szesnastkowym.

### Parametry

- `targetEUI` (String): Unikalny identyfikator docelowego urządzenia.
- `payload` (String): Dane w formacie szesnastkowym, które mają być wysłane jako część komendy.
- `overwrite` (Boolean): Flaga wskazująca, czy unieważnić wcześniejsze (jeszcze nie przekazane) komendy..

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
var targetEUI = "00124B0004F12345";
var payload = "00FFAA01";
var overwrite = true;

sgx.addHexCommand(targetEUI, payload, overwrite);
```

## <a name="addnotification"></a>`addNotification(newType, newMessage)`

Funkcja `addNotification` służy do dodawania nowej notyfikacji.

### Parametry

- `newType` (String): Typ nowej notyfikacji. Akceptowane wartości: `info`,`warning`,`alert`.
- `newMessage` (String): Treść nowej notyfikacji.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.addNotification("info", "Device activated successfully.");
```

## <a name="addvirtualdata"></a>`addVirtualData(newEUI, newName, newValue)`

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

## <a name="getaverage"></a>`getAverage(channelName, scope, newValue)`

Funkcja `getAverage` służy do uzyskiwania średniej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Średnia wartość dla danego kanału.

### Przykład użycia

```javascript
var average = sgx.getAverage("temperature", 10);
var newAverage = sgx.getAverage("temperature", 10, 23.0);
```

## <a name="getminimum"></a>`getMinimum(channelName, scope, newValue)`

Funkcja `getMinimum` służy do uzyskiwania minimalnej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Minimalna wartość dla danego kanału.

### Przykład użycia

```javascript
var minimum = sgx.getMinimum("temperature", 10);
var newMinimum = sgx.getMinimum("temperature", 10, 18);
```

## <a name="getmaximum"></a>`getMaximum(channelName, scope, newValue)`

Funkcja `getMaximum` służy do uzyskiwania maksymalnej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Maksymalna wartość dla danego kanału.

### Przykład użycia

```javascript
var maximum = sgx.getMaximum("temperature", 10);
var newMaximum = sgx.getMaximum("temperature", 10, 27);
```

## <a name="getsum"></a>`getSum(channelName, scope, newValue)`

Funkcja `getSum` służy do uzyskiwania sumy wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `scope` (Number): Zakres wartości.
- `newValue` (Number, opcjonalnie): Nowa wartość do uwzględnienia w obliczeniach.

### Zwraca

- `Number`: Suma wartości dla danego kanału.

### Przykład użycia

```javascript
var sum = sgx.getSum("temperature", 10);
var newSum = sgx.getSum("temperature", 10, 22);
```



## <a name="getlastvalue"></a>`getLastValue(channelName, skipNull)`

Funkcja `getLastValue` służy do uzyskiwania ostatniej wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `skipNull` (Boolean): Pomiń wartości `null`. Parametr opcjonalny.

### Zwraca

- `Mixed`: Ostatnia wartość dla danego kanału lub `null`, jeśli brak danych.

### Przykład użycia

```javascript
var lastValue = sgx.getLastValue("temperature");
```

## <a name="getlastdata"></a>`getLastData(channelName, skipNull)`

Funkcja `getLastData` służy do uzyskiwania ostatnich danych dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.
- `skipNull` (Boolean): Pomiń wartości `null`. Parametr opcjonalny. W przypadku jego braku `skipNull==false`.

### Zwraca

- `Object`: Ostatnie dane dla danego kanału.

### Przykład użycia

```javascript
var lastData = sgx.getLastData("temperature");
```

## <a name="getmodulo"></a>`getModulo(value, divider)`

Funkcja `getModulo` służy do uzyskiwania reszty z dzielenia wartości przez dzielnik.

### Parametry

- `value` (Number): Wartość do podzielenia.
- `divider` (Number): Dzielnik.

### Zwraca

- `Number`: Reszta z dzielenia.

### Przykład użycia

```javascript
var modulo = sgx.getModulo(10, 3); // 1
```

## <a name="getoutput"></a>`getOutput()`

Funkcja `getOutput` służy do uzyskiwania wyników przetwarzania.

### Zwraca

- `Mixed`: Wynik przetwarzania.

### Przykład użycia

```javascript
var output = sgx.getOutput();
```

## <a name="gettimestamp"></a>`getTimestamp(channelName)`

Funkcja `getTimestamp` służy do uzyskiwania znacznika czasu dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Number`: Znacznik czasu dla danego kanału.

### Przykład użycia

```javascript
var timestamp = sgx.getTimestamp("temperature");
```

## <a name="gettimestamputc"></a>`getTimestampUTC(y, m, d, h, min, s)`

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
var timestampUTC = sgx.getTimestampUTC(2024, 6, 5, 12, 0, 0);
```

## <a name="getvalue"></a>`getValue(channelName)`

Funkcja `getValue` służy do uzyskiwania wartości dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `Mixed`: Wartość dla danego kanału lub `null`, jeśli brak danych.

### Przykład użycia

```javascript
var value = sgx.getValue("temperature");
```

## <a name="getstringvalue"></a>`getStringValue(channelName)`

Funkcja `getStringValue` służy do uzyskiwania wartości tekstowej dla danego kanału.

### Parametry

- `channelName` (String): Nazwa kanału.

### Zwraca

- `String`: Wartość tekstowa dla danego kanału lub `null`, jeśli brak danych.

### Przykład użycia

```javascript
var stringValue = sgx.getStringValue("temperature");
```

## <a name="put"></a>`put(name, newValue, timestamp)`

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

### Uwagi

Użycie funkcji `put` wyłącza mechanizm automatycznego akceptowania i zapisywania w bazie odebranych danych. Jeśli w kodzie procesora danych zostanie użyta funkcja `put` to w bazie 
zostaną zarejestrowane jedynie dane przekazane w funkcjach `put` oraz `accept`.

### Przykład użycia

```javascript
// Signomix odebrał request z danymi o nazwach `temperature` i `humidity`, jednak w skrypcie 
// procesora danych chcemy dodać jeszcze wartość danej `pressure`
sgx.put("pressure", 1000)
// bez poniższych linii w bazie zostaną zapisane wartości null dla `temperature` oraz `humidity`
sgx.accept("temperature")
sgx.accept("humidity")
```

Patrz też: [accept](#accept)

## <a name="setstate"></a>`setState(newState)`

Funkcja `setState` służy do ustawiania nowego stanu urządzenia.

### Parametry

- `newState` (String): Nowy stan urządzenia.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.setState("active");
```

## <a name="setstatus"></a>`setStatus(newStatus)`

Funkcja `setStatus` służy do ustawiania nowego statusu urządzenia.

### Parametry

- `newStatus` (String): Nowy status urządzenia.

### Zwraca

- `void`: Funkcja nie zwraca żadnej wartości.

### Przykład użycia

```javascript
sgx.setStatus("offline");
```

## <a name="reversehex"></a>`reverseHex(hexStr)`

Funkcja `reverseHex` służy do odwracania kolejności znaków w łańcuchu szesnastkowym.

### Parametry

- `hexStr` (String): Łańcuch szesnastkowy.

### Zwraca

- `String`: Odwrócony łańcuch szesnastkowy.

### Przykład użycia

```javascript
var reversedHex = sgx.reverseHex("00FFAA01"); // "01AAFF00"
```

## <a name="swap32"></a>`swap32(val)`

Funkcja `swap32` służy do zmiany kolejności bajtów w liczbie 32-bitowej.

### Parametry

- `val` (Number): Liczba 32-bitowa.

### Zwraca

- `Number`: Liczba z zmienioną kolejnością bajtów.

### Przykład użycia

```javascript
var swapped = sgx.swap32(0x12345678); // 0x78563412
```

## <a name="distance"></a>`distance(latitude1, longitude1, latitude2, longitude2)`

Funkcja `distance` służy do obliczania odległości między dwoma punktami geograficznymi.

### Parametry

- `latitude1` (Number): Szerokość geograficzna punktu 1.
- `longitude1` (Number): Długość geograficzna punktu 1.
- `latitude2` (Number): Szerokość geograficzna punktu 2.
- `longitude2` (Number): Długość geograficzna punktu 2.

### Zwraca

- `Number`: Odległość między dwoma punktami w metrach.

### Przykład użycia

```javascript
// odległość pomiędzy dwoma punktami
var dist = sgx.distance(52.2296756, 21.0122287, 41.8919300, 12.5113300);

// odległość punktu od przesłanej lokalizacji
var dist = sgx.distance(2.2296756, 21.0122287, sgx.getValue("latitude"), sgx.getValue("longitude") );
```

## <a name="homeDistance"></a>`homeDistance(latitude, longitude)`

Funkcja `homeDistance` służy do obliczania odległości między danym punktem geograficznym,
a punktem położenia urządzenia zapisanym w jego konfiguracji.

### Parametry

- `latitude` (Number): Szerokość geograficzna punktu.
- `longitude` (Number): Długość geograficzna punktu.


### Zwraca

- `Number`: Odległość między dwoma punktami w metrach.

### Przykład użycia

```javascript
// odległość podanego punktu od lokalizacji podanej w konfiguracji urządzenia
var dist = sgx.homeDistance(41.8919300, 12.5113300);

// odległość przesłanej lokalizacji od lokalizacji podanej w konfiguracji urządzenia
var dist = sgx.homeDistance( sgx.getValue("latitude"), sgx.getValue("longitude") );
```
