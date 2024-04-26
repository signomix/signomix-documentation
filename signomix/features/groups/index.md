# Grupy urządzeń

Grupa ułatwia odwoływanie się do listy urządzeń mających podobne parametry i przeznaczenie. 

## Konfiguracja
Definiujemy ją podając:
- uinikalny identyfikator (EUI) grupy
- nazwę
- listę nazw pomiarów oddzielonych przecinkami
- zespół - lista loginów użytkowników mających dostęp read only do tej grupy
- administratorów - lista loginów użytkowników mających pełny dostęp do tej grupy

Urządzenie przypisyjemy do grupy podając jej nazwę przy definiowaniu tego urządzenia.

**Uwaga!**<br>
Przypisując urządzenie do grupy należy zwrócić uwagę na listę nazw pomiarów. Jeśli lista nazw pomiarów zdefiniowanych dla grupy nie jest podzbiorem takiej listy w przypisywanym urządzeniu, to przypisanie to nie będzie najprawdpodobniej 
przydatne.

## Pobieranie daych grupy

Dane przesłane przez urządzenia grupy można pobrać jako plik w formacie CSV. Zakres pobieranych danych jest ograniczony do 31 dni wstecz od wybranej daty końcowej.