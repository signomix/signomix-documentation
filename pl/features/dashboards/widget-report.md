# Kontrolka `Tabela z danymi`

Prezentuje tabelaryczne zestawienie danych zarejestrowanych przez jedno źródło lub przez grupę źródeł danych.

<img src="../../assets/table-report.png" class="border rounded shadow mt-1 mb-3" width="100%" >
<!--
<img class="border rounded shadow mt-1 mb-3" width="40%" src="/api/file?path=signomix-documentation/features/dashboards/table-report.png">
-->

## Konfigurowanie

- **Tytuł** - tytuł tabeli
- **Nazwy na kontrolce** - nazwy kolumn tabeli stosowane (jeśli podane) zamiast nazw kanałów danych w definicji raportu 
- **Zakres danych (DQL)** - definicja raportu pobierającego dane
- **Zaokrąglenie wartości** - liczba miejsc po przecinku dla wartości prezentowanych w tabeli

Przykładowa definicja zakresu danych:
```
report DqlReport group myGroupEui channel pm2_5avg,pm10avg,temperature last 1
```