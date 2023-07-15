# Czas odświeżania pulpitu
Pulpit jest odświeżany automatycznie w stałych odstępach czasu. Każda pokazywana na nim kontrolka pobiera 
w trakcie tego procesu dane, zgodnie z jego konfiguracją.

# Konfigurowanie czasu odświeżania
Domyślnie pulpit jest odświeżany co 5 minut.

Czas odświeżania może być zdefiniowany w ustawieniach [aplikacji](/pl/app/applications.md) o nazwie "system". Przykład konfiguracji:

```
{
    "refreshInterval": 7000
}
```
