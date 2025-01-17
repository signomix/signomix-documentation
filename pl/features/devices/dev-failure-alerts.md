# Powiadamianie o awariach urządzeń

Jedną z funkcjonalności Signomiksa jest wykrywanie przerw w działaniu źródeł danych lub urządzeń. 

Serwis raportuje jako problem sytuacje, gdy dane źródło dane przestaje przesyłać komunikaty z danymi.

Mechanizm wykrywania takich problemów uwzględnia źródła danych, które:
- są oznaczone jako aktywne,
- mają w konfiguracji zadeklarowany interwał transmisji danych większy od zera,
Jako problem raportowane są sytuacje, gdy urządzenie pominie minimum dwie kolejne transmisje.

## Sposób działania

Wykrywanie problemów jest uruchamiane cyklicznie z częstotliwością uzależnioną od rodzaju konta użytkownika:
- co 20 minut dla kont darmowych 
- co 10 minut dla kont płatnych

Różna częstotliwość uruchamiania wykrywania problemów oraz interwałów transmisji przypisanych urządzeniu powoduje, że czas mijający od momentu zaistnienia awarii urządzenia do zaraportowania problemu użytkownikowi będzie różny w zależności od typu konta.

Dla kont darmowych:

- od 20 do 40 minut -> jeśli urządzenie przesyła dane częściej niż co 20 minut 
- 2 * interwał transmisji + maksymalnie 20 minut -> jeśli urządzenie przesyła rzadziej niż co 20 minut 

Dla kont płatnych:

- od 10 do 20 minut -> jeśli urządzenie przesyła dane częściej niż co 10 minut 
- 2 * interwał transmisji + maksymalnie 10 minut -> jeśli urządzenie przesyła rzadziej niż co 10 minut 

## Sposób powiadamiania użytkowników

Wykryte problemy są raportowane użytkownikom:
- właścicielowi urządzenia (użytkownikowi, który je zarejestrował),
- członkowi zaspołu polu (wpisanymi w polu `zespół` konfiguracji urządzenia), 
- administratorom urządzenia (wpisanymi w polu `administratorzy` konfiguracji urządzenia). 

Historia problemów z działaniem urządzeń jest udostępniana użytkownikowi po zalogowaniu się do webaplikacji w menu `Infrastruktura > Komunikaty`. 

Powiadomienia mogą być również wysyłane jako e-mail, SMS lub do zewnętrznego serwisu (webhook) 