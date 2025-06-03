# Konto użytkownika - ustawienia

Parametry konta użytkownika można przeglądać po wybraniu z menu aplikacji opcji `Ustawienia`. W celu zmiany tych parametrów należy kliknąć ikonę TODO.
Formularz zmiany ustawień pozwala na zmianę parametrów:

- imię,
- nazwisko,
- adres e-mail,
- prefix numeru telefonu (numer kierunkowy kraju),
- preferowany język aplikacji,
- konfigurację kanałów powiadomień.

Patrz także: [Typy kont](account_types.md).

## Kanały powiadomień

Powiadomienia wysyłane przez Signomix dzielą się na 3 typy, których nazwy sugerują ich przeznaczenie:
- informacyjne - zwykłe informacje dotyczące działania urządzeń użytkownika lub platformy
- ostrzegawcze - ostrzeżenia
- alarmy o wystąpieniu problemów o charakterze krytycznym

Dla każdego z powyższych typów powiadomień można skonfigurować kanał komunikacji, którym Signomix prześle powiadomienie do użytkownika. W każdym przypadku powiadomienia będą dostępne do przeglądania w aplikacji webowej (opcja menu `Powiadomienia`). Użytkownik może wybrać:
- W aplikacji - powiadomienia będą dostępne wyłącznie w aplikacji webowej,
- E-mail - powiadomienia zostaną wysłane na podany adres e-mail,
- Webhook - powiadomienia zostaną wysłane zapytaniem HTTP na podany adres,
- SMS - wiadomość SMS wysyłana na ustalony numer telefonu

### Powiadomienia SMS

Powiadomienia SMS są dostępne dla użytkowników kont płatnych.

Reguły:
- Domyślnym prefiksem telefonu (jeśli nie został podany) jest "+48".
- Przy wysyłaniu SMS numer telefonu zostaje zawsze poprzedzony prefiksem.
- Wysłanie SMS zmniejsza pulę punktów dla usług dodatkowych użytkownika o 2 punkty.
- Konto płatne ma do dyspozycji pulę 20 punktów na miesiąc.
- Zwiększenie puli punktów wymaga odrębnego zakupu.

### Konfiguracja kanału Webhook

Składnia dla adresu Webhook: `[[HeaderName:]HeaderValue@]ServiceURI`

Znaczenie:

|element|meaning|
|---|---|
|HeaderName|Nazwa nagłówka dodawanego do zapytania HTTP. Domyślna wartość to `Authorization`|
|HeaderValue|Wartość zadeklarowanego nagłówka|
|ServiceURI|Adres serwisu, do którego będzie wysłane powiadomienie|

Powiadomienia są wysyłane metodą POST. Przykład symulacji wysyłanego żądania przy użyciu programu cURL:

```shell
curl  -X POST \
  'https://mywebhookservice.com' \
  --header 'Authorization: token' \
  --header 'Content-Type: text/plain' \
  --data-raw 'notification text'
```

> **UWAGA!** Nie należy dodawać nagłówka `Content-Type`. Zostanie od dodany automatycznie na podstawie zawartości powiadomienia.

