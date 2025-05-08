# Kontrolka `Mapa grupowa`

<img src="../../assets/multimap.png" class="border rounded shadow mt-1 mb-3" width="30%">

## Konfigurowanie

- **Tytuł**- tytuł wykresu (informacyjnie, nie jest wyświetlany)
- **Zakres danych (DQL)** - definicja zakresu danych pobieranych z grupy źródeł (urządzeń)
- **Reguła alarmu** - deficja określająca kolory ostrzeżeń dla punktów na mapie

Przykładowa definicja zakresu danych:
```
report DqlReport group myGroupEui channel gps_lat,gps_lon,pm2_5avg,pm10avg,temperature,humidity,pressure last 1
```

## Konfiguracja nazw koordynat

Jeżeli źródło danych przesyła koordynaty używając innych nazw pomiarów niż `latitude` i `longitude`, to konieczne jest dodanie do definicji kontrolki konfiguracji tych nazw. Poniżej przykład:

```json
{
"latitudeName": "gps_lat",
"longitudeName":"gps_lon"
}
```