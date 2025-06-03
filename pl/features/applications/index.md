# Aplikacje

<span class="badge bg-primary">Funkcjonalność dostępna dla organizacji</span>

Aplikacje mogą być tworzone i modyfikowane jedynie przez użytkownika będącego administratorem systemu.

## Parametry aplikacji

Każdy z parametrów aplikacji jest opcjonalny.

### Identyfikator (ID)

Identyfikator jest tworzony automatycznie.

### Nazwa
Nazwa jest prezentowana na liście aplikacji.

### Skrypt dekodera danych

Kod JavaScript służący do odkodowania danych przychodzących ze źródła danych. Jeśli jest tutaj podany, to zastąpi skrypt z konfiguracji źródła danych połączonej z tą aplikacją.

### Skrypt procesora danych

Kod wykorzystywany do przetwarzania danych przychodzących ze źródła danych. Jeśli jest tutaj podany, to zastąpi skrypt z konfiguracji źródła danych połączonej z tą aplikacją.
Może to być kod w języku JavaScript lub Python.

### Konfiguracja

Jest to lista właściwości zapisana w formacie obiektu JSON. Przykład:

```json
{
    "refreshInterval": 300
}
```

### Opis

Opis aplikacji jest opcjonalny, jednak warto w nim zawrzeć krótką informację o jej przeznaczeniu i sposobie użycia.

