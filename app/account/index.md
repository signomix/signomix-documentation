# Konto użytkownika - ustawienia

Parametry konta użytkownika można przeglądać po wybraniu z menu aplikacji opcji `Ustawienia`. W celu zmiany tych parametrów należy kliknąć ikonę TODO.
Formularz zmiany ustawień pozwala na zmianę parametrów:

- imię,
- nazwisko,
- adres e-mail,
- prefix numeru telefonu (numer kierunkowy kraju),
- preferowany język aplikacji,
- konfigurację kanałów powiadomień.

## Kanały powiadomień

Powiadomienia wysyłane przez Signomix dzielą się na 4 typy, których nazwy sugerują ich przeznaczenie:
- ogólne - powiadomienia dotyczących platformy, np. komunikatów administratora
- informacyjne - zwykłe informacje dotyczące działania urządzeń użytkownika lub platformy
- ostrzegawcze - ostrzeżenia
- alarmy o wystąpieniu problemów o charakterze krytycznym

Dla każdego z powyższych typów powiadomień można skonfigurować kanał komunikacji, którym Signomiks prześle powiadomienie do użytkownika. W każdym przypadku powiadomienia będą dostępne do przeglądania w aplikacji webowej (opcja menu `Powiadomienia`). Użytkownik może wybrać:
- W aplikacji - powiadomienia będą dostępne wyłącznie w aplikacji webowej,
- E-mail - powiadomienia zostaną wysłane na podany adres e-mail,
- Webhook - powiadomienia zostaną wysłane zapytaniem HTTP na podany adres.

### Konfiguracja kanału Webhook

Składnia dla adresu Webhook: `[[HeaderName:]HeaderValue@]ServiceURI`

Znaczenie:
|element|meaning|
|---|---|
|HeaderName|Nazwa nagłówka dodawanego do zapytania HTTP. Domyśna wartość to `Authorization`|
|HeaderValue|Wartość zadeklarowanego nagłówka|
|ServiceURI|Adres serwisu, do którego będzie wysłane powiadomienie|

> **UWAGA!** Nie należy dodawać nagłówka `Content-Type`. Zostanie od dodany automatycznie na podstawie zawartości powiadomienia.

