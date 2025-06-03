# White labelling

<span class="badge bg-primary">Funkcjonalność dostępna dla organizacji</span>

Webaplikacja Signomix umożliwia dostosowanie wyglądu memu do wymagań organizacji poprzez zdefiniowanie:
- nazwy organizacji wyświetlanej na górnej belce webaplikacji,
- kolorów tła i tekstu dla górnej belki webaplikacji,
- adresu url wyświetlanego logo.

Dodatkowo administrator może określić czy w menu pojawią się opcje:
- odnośnik do dokumentacji ogólnej Signomiksa,
- odnośnik do dokumentacji dla członków organizacji (help).

Przykładowa konfiguracja:
```json
{
    "name": "My comp. Sp. z o.o.", 
    "logo_url": "https://mycomp.com/logo.png", 
    "background_color": "2b1a17", 
    "text_color": "#f8f9fa", 
    "menu_documentation": true,
    "menu_help": true, 
}
```