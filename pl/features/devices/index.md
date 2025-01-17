# Źródła danych (urządzenia) 

Źródłem danych dla może być dowolny obiekt (urządzenie fizyczne lub oprogramowanie) 
dostarczający dane pomiarowe za pomocą udostępnianych przez Signomiksa API.

Z uwagi na sposób komunikacji mogą to być:

- urządzenia LoRaWAN pracujące w sieci The Things Network,
- urządzenia LoRaWAN pracujące w sieci ChirpStack,
- urządzenia lub oprogramowanie przesyłające dane korzystając z protokołu HTTP.

Po odebraniu zapytania przez REST API Signomiks obsługuje je kierując najpierw do dekodera danych, a następnie do procesora danych i zapisuje je do bazy danych.
- [Funkcje biblioteki procesora danych](data_processor_lib.md)

Signomiks może wykrywać awarie urządzeń powodujące, że dane pomiarowe przestają być rejestrowane.
- [Powiadamianie o awariach urządzeń](dev-failure-alerts)