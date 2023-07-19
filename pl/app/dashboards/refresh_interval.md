# Czas odświeżania pulpitu
Pulpit jest odświeżany automatycznie w stałych odstępach czasu. Każda pokazywana na nim kontrolka pobiera 
w trakcie tego procesu dane, zgodnie z jego konfiguracją.

## Konfigurowanie czasu odświeżania
Domyślnie pulpit jest odświeżany co 5 minut.

Czas odświeżania (liczba sekund) może być zdefiniowany w ustawieniach [aplikacji](/pl/app/applications/intro.md) o nazwie "system". Przykład konfiguracji:

```
{
    "refreshInterval": 300
}
```

## Konfigurowanie czasu odświeżania dla organizacji

W przypadku użytkowników należących do organizacji innej niż domyślna czas odświeżania może być skonfigurowany
w zdefiniowanej w ramach tej organizacji aplikacji "system". Jeżeli takiej nie ma, to obowiązuje konfiguracja z aplikacji "system" organizacji domyślnej.