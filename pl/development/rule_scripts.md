# Skrypty reguł

W przypadku zaznaczenia podczas definiowania reguły opcji "Użyj skryptu", użytkownik może wpisać własny kod funkcji, która będzie wykonywana w ramach reguły. Funkcja języka Python musi mieć nazwę `checkRule`, nie przyjmować żadnych argumentów oraz zwracać wartość typu string.

```python
def checkRule():
    return ""
```

### Dokumentacja dla programisty: Implementacja funkcji `checkRule`

#### Cel funkcji

Funkcja `checkRule` jest głównym miejscem, w którym należy zaimplementować logikę sprawdzania warunków alarmowych lub reguł dla urządzenia IoT w systemie Signomix Sentinel. Funkcja ta powinna korzystać z udostępnionych narzędzi do pobierania wartości pomiarów i zwracać wynik w określonym formacie.

---

#### Kontekst i dostępne narzędzia

W środowisku skryptowym masz dostęp do następujących zmiennych i funkcji pomocniczych:

- **Obiekty globalne:**
  - `config` – konfiguracja sentinela (np. parametry reguł)
  - `device` – obiekt urządzenia (np. `device.EUI`)
  - `valuesArr` – lista wartości pomiarów dla urządzenia
  - `channelMap` – mapa kanałów pomiarowych urządzenia

- **Funkcje pomocnicze:**
  - `getValue(measurement)` – pobiera ostatnią wartość wskazanego pomiaru dla bieżącego urządzenia
  - `get_measurementIndex(eui, measurement, deviceChannelMap)` – zwraca indeks pomiaru w strukturze danych
  - `get_value(eui, measurement, values, deviceChannelMap)` – pobiera wartość pomiaru dla wskazanego urządzenia
  - `get_delta(eui, measurement, values, deviceChannelMap)` – pobiera przyrost (delta) wartości pomiaru dla wskazanego urządzenia
  - `conditionsMet(measurement, value)` – zwraca sformatowany wynik, gdy warunek jest spełniony
  - `conditionsMetWithCommand(measurement, value, commandTarget, command)` – jak wyżej, z dodatkową komendą
  - `conditionsNotMet()` – zwraca pusty wynik, gdy warunek nie jest spełniony

---

#### Wymagania dotyczące funkcji `checkRule`

- Funkcja **nie przyjmuje argumentów**.
- Funkcja **musi zwracać string**:
  - Jeśli warunki są spełnione: użyj `conditionsMet(...)` lub `conditionsMetWithCommand(...)`
  - Jeśli warunki nie są spełnione: użyj `conditionsNotMet()`
- Funkcja powinna korzystać z funkcji pomocniczych do pobierania wartości pomiarów.
- Możesz implementować dowolną logikę warunkową, np. porównania, operacje matematyczne, złożone reguły.

---

#### Przykład prostej implementacji

```python
def checkRule():
    v1 = getValue("temperature")
    v2 = getValue("humidity")
    if v1 is None or v2 is None:
        return conditionsNotMet()
    if v2 - v1 > 10:
        return conditionsMet("temperature", v1)
    return conditionsNotMet()
```

---

#### Przykład z komendą

```python
def checkRule():
    temp = getValue("temperature")
    if temp is not None and temp > 30:
        return conditionsMetWithCommand("temperature", temp, "fan", "ON")
    return conditionsNotMet()
```

---

#### Uwagi

- Funkcja powinna być **czysta** – nie modyfikuj globalnych struktur, poza odczytem danych.
- Jeśli potrzebujesz innych pomiarów lub logiki, możesz korzystać z przekazanych obiektów i funkcji.
- Wynik funkcji jest interpretowany przez system – format stringa jest istotny.

---

#### Debugowanie

- Możesz używać `javaLogger.info("...")` do logowania informacji podczas działania skryptu.
- Jeśli funkcja nie zwraca oczekiwanego wyniku, sprawdź czy pobierane wartości nie są `None`.

---

**Podsumowanie:**
Twoim zadaniem jest zaimplementowanie funkcji `checkRule`, która na podstawie danych pomiarowych i logiki biznesowej zwraca odpowiedni string informujący system o spełnieniu lub niespełnieniu warunku. Wykorzystuj dostępne funkcje pomocnicze i dbaj o czytelność kodu.
