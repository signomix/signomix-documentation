# Kontrolka typu `Wykres`

Kontrolka prezentuje wykres budowany na podstawie serii danych z jednego lub więcej rodzajów pomiarów.

# Konfigurowanie

**Tytuł** - tytuł wykresu
**Zakres danych (DQL)** - definicja raportu pobierającego dane do wykresu
**Typ wykresu** - do wyboru: liniowy, słupkowy, punktowy
**Pokazuj znaczniki** - na wykresie liniowym zostaną oznaczone punkty pobrania danych
**Zaznacz obszar** - obszar pod wykresem liniowym zostanie wypełniony odpowiednim kolorem
**Czas na osi X** - jaka jednostka czasu zastanie zastosowana dla osi X ()
**Opcje osi** - udostępnia dodatkowe parametry dla osi wykresu
**Automatycze skalowanie dla osi Y** - minimum i maksimum osi Y zostanie wyznaczone na podstawie wyświetlanych danych

Przykład definicji zakresu danych:
```
report DqlReport eui ROOM1 channel temperature,status,device_status limit 10
```
Znaczenie:
- report - słowo kluczowe, po którym występuje nazwa klasy raportu
- DqlReport - predefiniowana, uniwersalna klasa raportu obsługująca składnię DQL
- eui - słowo kluczowe, po którym występuje identyfikator źródła danych (urządzenia)
- channel - słowo kluczowe, po którym występuje lisa nazw pomiarów (kanałów danych) przesyłanych przez dane źródło
- limit - liczba ostatnich pomiarów, które będą prezentowane

Patrz też: [Data Query Language](/development/dql.md)