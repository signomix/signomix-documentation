# Konfigurowanie działania webaplikacji

<span class="badge bg-primary">Funkcjonalność dostępna dla organizacji</span>

Działanie i wygląd webaplikacji Signomix można dostosować do wymagań organizacji poprzez:
- podanie nazwy organizacji wyświetlanej w górnej belce webaplikacji
- podanie adresu URL do pliku logo organizacji
- wybranie koloru tekstu oraz tła górnej belki webaplikacji
- skonfigurowanie widoczności wybranych elementów menu:
  - odnośnik do dokumentacji ogólnej Signomiksa
  - odnośnik do dokumentacji dla członków organizacji (Pomoc)
- wybranie pulpitu, który będzie domyślnie wyświetlany jako strona główna

Przykładowe ustawienia:

```json
{
  "name": "Signomix Demo",
  "logo_url": "https://frog01-20608.wykr.es/img/demo-logo.png",
  "text_color": "#f8f9fa",
  "background_color": "2b1a17",
  "menu_help": true,
  "menu_documentation": true,
  "mainDashboard": "S-0123456789"
}
```
