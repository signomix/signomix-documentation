# Predefiniowane raporty

W ramach funkcjonalności [serwera raportów](/administration/report_server.md) Signomiks udostępnia zestaw predefiniowanych raportów, opisanych poniżej.

LISTA BĘDZIE ROZWIJANA W PRZYSZŁOŚCI

## Raport logowań

Prezentuje listę logowań użytkownika do Signomiksa.
Raport może być użyty na pulpicie za pośrednictwem kontrolki [Tabela z danymi](/features/dashboards/widget-report.md).

Konfiguracja kontrolki wymaga podania nazwy klasy raportu w poli `Zakres danych`.

Przykład pobierający dane 10 ostatnich logowań:

```
last 10 report UserLoginReport
```

## Raport DQL

Dostarcza danych pomiarowych na podstawie specyfikacji opisaną ze składnią DQL.

