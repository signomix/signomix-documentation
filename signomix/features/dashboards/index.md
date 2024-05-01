# Pulpity

Dane zebrane pozyskane z urządzeń można zaprezentować na pulpicie zawierającym wybrane kontrolki. Pojedyncza kontrolka, 
zależnie od jej typu, może prezentować dane pochodzące z jednego lub więcej urządzeń.

Położenie i rozmiar kontrolek można wygodnie zmieniać z użyciem mechanizmu drag and drop.

## Dostępne typy kontrolek

|Typ|Co przedstawia|
|---|---|
|[chart](widget-chart.md)|Wykres|
|[date](widget-date.md)|Prezentacja daty|
|[devinfo](widget-devinfo.md)|Opis urządzenia|
|[image](widget-image.md)|Obraz|
|[led](widget-led.md)|Kontrolka LED| 
|[link](widget-link.md)|Odnośnik|
|[map](widget-map.md)|Mapa pokazująca położenie lub trasę urządzenia|
|[multimap](widget-multimap.md)|Mapa pokazująca położenie wielu urządzeń|
|[multitrack](widget-multitrack)|Mapa z trasami wielu urządzeń|
|[plan](widget-plan.md)|Plan lub schemat z danymi|
|[raw](widget-raw.md)|Dane w formacie JSON|
|[report](widget-report.md)|Tabelaryczne zestawienie danych|
|[symbol](widget-symbol.md)|Ostatnia zarejestrowana wartość|
|[stopwatch](widget-stopwatch.md)|Stoper|
|[time](widget-time.md)|Prezentacja czasu|
|[text](widget-text.md)|Treść tekstowa|

## Uprawnienia

Użytkownik będący autorem pulpitu może go później dowolnie oglądać oraz modyfikować. Definiując pulpit można również 
wskazać (poprzez podanie listy loginów użytkowników oddzielonych przecinkami):

- zespół - osoby mogące oglądać pulpit
- administratorów - osoby mogące oglądać oraz modyfikować pulpit.

## Publikowanie pulpitów

Definiując pulpit można również oznaczyć go jako "publiczny" i wtedy:

- pulpit jest publicznie dostępny do oglądania w webaplikacji `view.signomix.com` dla każdej osoby znającej unikalny odnośnik do niego,
- dane wszystkich urządzeń, do których ten pulpit się odwołuje, stają się również w pełni **dostępne dla osób znających odnośnik do pulpitu**

Z powyższych względów podejmując decyzję o "upublicznieniu" pulpitu należy podjąć w pełni świadomie.


