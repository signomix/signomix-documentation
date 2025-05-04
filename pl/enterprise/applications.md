# Aplikacje

Aplikacja składa się z definicji:
- skryptu dekodera danych
- skryptu procesora danych
- konfiguracji

Aplikacje mogą być definiowane dla:
- wszystkich użytkowników platformy - przez administratora platformy,
- organizacji - przez administratora organizacji.

## Definiowanie obsługi źródeł danych

Konfigurując źródło danych można podać identyfikator aplikacji, która będzie dla niego zastosowana. W takim wypadku kody aplikacji będą użyty do dekodowania oraz przetwarzania odbieranych z tego źródła danyc.

Planując instalowanie wielu urządzeń tego samego typu można zdefiniować dla nich aplikację i w ten sposób:
- uniknąć konieczności wielokrotnego definiowania skryptów dekodera i procesora danych,
- zapewnić jednolite algorytmy przetwarzania danych,
- umożliwić łatwe zmiany tych algorytmów w razie potrzeby. 