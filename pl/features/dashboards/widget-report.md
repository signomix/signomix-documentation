# Kontrolka `Tabela z danymi`

Prezentuje tabelaryczne zestawienie danych zarejestrowanych przez jedno źródło lub przez grupę źródeł danych.

<img src="../../assets/table-report.png" class="border rounded shadow mt-1 mb-3" width="100%" >
<!--
<img class="border rounded shadow mt-1 mb-3" width="40%" src="/api/file?path=signomix-documentation/features/dashboards/table-report.png">
-->

## Definicja kontrolki

### Podstawowa

- **Tytuł** - tytuł tabeli
- **Typ** - typ raportu (tabela z danymi)
- **Źródło danych** - Grupa urządzeń lub Raport - **Raport** pozwala na zdefiniowanie własnego zakresu danych (DQL) i jest zalecany do stosowania
- **Rozmiar na urządzaniach mobilnych** - liczba wierszy zajmowana przez kontrolkę na urządzeniach mobilnych
- **Pozycja na urządzaniach mobilnych** - pozycja kontrolki na urządzeniach mobilnych licząc od góry (na urządzaniach mobilnych kontrolki są układane jedna pod drugą)

### Szczgóły
- **Nazwy na kontrolce** - nazwy kolumn tabeli stosowane (jeśli podane) zamiast nazw kanałów danych w definicji raportu 
- **Zakres danych (DQL)** - definicja raportu pobierającego dane
- **Zaokrąglenie wartości** - liczba miejsc po przecinku dla wartości prezentowanych w tabeli
- **Rola użytkownika** - jeśli podana, kontrolka będzie widoczna tylko dla użytkowników z określoną rolą

Przykładowa definicja zakresu danych:
```
report DqlReport group myGroupEui channel pm2_5avg,pm10avg,temperature last 1
```

### Konfiguracja

Zakładka pozwala na podanie dodatkowych ustawień kontrolki. Konfiguracja jest opcjonalna i musi mieć postać poprawnego dokumentu JSON.

Poniżej przykład konfiguracji z pełnym zestawem dostępnych opcji. Poszczególne elementy JSON'a są opcjonalne.

Przykład ma format JSONC (z komentarzami). Konfigurację dla własnej kontrolki należy podać bez komentarzy.

```json
// -*- jsonc -*-
{
"selectionColumn": "eui", // nazwa kolumny wg której nastąpi zaznaczenie wierszy (np. eui, name))
"sortColumn":"name", // nazwa kolumny wg której nastąpi domyślne sortowanie wierszy
"dashboardID": "S-0000019A2F97ED0E", // ID pulpitu do którego nastąpi przekierowanie wybraniu zestawu wierszy
"euiVisible": false, // czy kolumna EUI ma być widoczna w tabeli
"timeVisible": true, // czy kolumna z czasem ma być widoczna w tabeli
"nameVisible":true, // czy kolumna z nazwą ma być widoczna w tabeli
"columnsVisible":true, // czy kolumny danych mają być widoczne w tabeli
"roundings": [0,1,1], // tablica z liczbą miejsc po przecinku dla poszczególnych kolumn danych
"dataTypes": ["number","number","number"], // tablica z typami danych dla poszczególnych kolumn danych (number, string, boolean)
"hideNaN": true // czy wartości NaN mają być ukrywane w tabeli
}
```

### Opis

Tu można podać dodatkowy opis kontrolki. Dla tego typu kontrolki opis ma charakter informacyjny i nie jest wyświetlany na pulpicie.

