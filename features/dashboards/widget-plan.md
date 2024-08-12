# Kontrolka typu `Plan`

Prezentuje schemat lub plan z naniesionymi na niego lokalizacjami oraz danymi wyb**ranych źródeł danych.

## Konfigurowanie

Konfigurując kontrolkę `Odnośnik' należy wypełnić pola:

- **Tytuł** - tekst wyświetlany na przycisku
- **Typ** - typ kontrolki: `Plan`
- **Nazwy pomiarów** - nazwy pomiarów, których wartości mają być pokazane
- **Nazwy na kontrolce** - nazwy w formie do wyświetlenia (np. przetłumaczone na inny język)
- **Grupa** - identyfikator (EUI) grupy źródeł danych, które mają być uwidocznione na planie
- **Opis** - definicja planu - kod źródłowy SVG

## Przykład

<img src="../../assets/plan.png" class="border rounded shadow mt-1 mb-3" width="30%">

## Kod źródłowy planu

Kod źródłowy SVG zdefiniowany w polu `Opis` kontrolki musi spełniać kilka reguł:

- kod SVG powinien być czysty (pure SVG, plain SVG) - nie powinien być uzależniony od dodatków wstawianych często przez zawansowane edytory (jak np. Inkscape, Adobe Ilustrator itp.) 
- kod musi zawierać definicję `viewbox` - patrz przykład poniżej

Należy również pamiętać, że koordynaty zdefiniowane dla źródeł danych będą interpretowane jako koordynaty wewnątrz `viewbox`, czyli nie są w tym wypadku koordynatami GPS. Przykładowo, źródło danych na ilustracji powyżej ma koordynaty (100,80).

```
<svg  xmlns="http://www.w3.org/2000/svg" version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink"
viewBox="0 0 1000 1000" transform="scale(1,1)">
    <rect x="4" y="2" width="980" height="663" fill="rgb(255, 255, 255)" stroke="black"/>
    <rect x="4" y="2" width="467.5" height="663" fill="rgb(255, 255, 255)" stroke="black"/>
    <rect x="4" y="2" width="467.5" height="250" fill="rgb(255, 255, 255)" stroke="black"/>
    <text textLength="93.2" font-size="26.7" x="10" y="30" fill="black">room1</text>
    <text textLength="93.2" font-size="26.7" x="10" y="280" fill="black">room2</text>
    <text textLength="93.2" font-size="26.7" x="480" y="30" fill="black">room3</text>
</svg>
```