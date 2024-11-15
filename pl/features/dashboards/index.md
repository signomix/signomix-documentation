# Pulpity

Dane zebrane pozyskane z urządzeń można zaprezentować na pulpicie zawierającym wybrane kontrolki. Pojedyncza kontrolka, 
zależnie od jej typu, może prezentować dane pochodzące z jednego lub więcej urządzeń.

Położenie i rozmiar kontrolek można wygodnie zmieniać z użyciem mechanizmu drag and drop.

## Dostępne typy kontrolek

|Typ|Co przedstawia|
|---|---|
|[Karta wartości](widget-symbol.md)|Ostatnia zarejestrowana wartość|
|[LED](widget-led.md)|Kontrolka LED| 
|[Mapa](widget-map.md)|Mapa pokazująca położenie lub trasę urządzenia|
|[Mapa grupowa](widget-multimap.md)|Mapa pokazująca położenie wielu urządzeń|
|[Obraz](widget-image.md)|Obraz|
|[Odnośnik](widget-link.md)|Odnośnik|
|[Plan](widget-plan.md)|Plan lub schemat z danymi|
|[Przycisk](widget-button.md)| Przycisk wysyłający polecenie|
|[Tabela z danymi](widget-report.md)|Tabelaryczne zestawienie danych|
|[Tekst](widget-text.md)|Treść tekstowa|
|[Informacje o źródle danych](widget-info.md)|Informacje o źródle danych (urządzeniu)|
|[Trasy grupowe](widget-multitrack)|Mapa z trasami wielu urządzeń|
|[Wykres](widget-chart.md)|Wykres|
|[Wykres grupowy](widget-groupchart.md)|Wykres grupowy|
|[Czas](widget-time.md)|Czasu pomiaru|
|[Data](widget-date.md)|Data pomiaru|
|[Stoper](widget-stopwatch.md)|Stoper|
<!--
|[Surowe dane](widget-raw.md)|Dane w formacie JSON|
-->

## Uprawnienia

Użytkownik będący autorem pulpitu może go później dowolnie oglądać oraz modyfikować. Definiując pulpit można również 
wskazać (poprzez podanie listy loginów użytkowników oddzielonych przecinkami):

- zespół - osoby mogące oglądać pulpit
- administratorów - osoby mogące oglądać oraz modyfikować pulpit.

## Publikowanie pulpitów

Definiując pulpit można również oznaczyć go jako "publiczny" i wtedy:

- pulpit jest publicznie dostępny do oglądania w webaplikacji `view.signomix.com` dla każdej osoby znającej unikalny odnośnik do niego,
- dane wszystkich urządzeń, do których ten pulpit się odwołuje, stają się również  **dostępne dla osób znających odnośnik do pulpitu**

Z powyższych względów podejmując decyzję o "upublicznieniu" pulpitu należy podjąć w pełni świadomie.


