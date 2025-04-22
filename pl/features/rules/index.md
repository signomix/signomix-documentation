# Reguły

Reguły definiują jakie akcje mają być wykonane w odpowiedzi na zdarzenia związane 
z przesyłaniem przez urządzenia
nowych danych. Spełnienie przez dane warunków określonych w regułach powoduje 
wygenerowanie w serwisie wiadomości 
określonego typu. <br> 
Reguły mogą być definiowane dla:
- wybranego urządzenia,
- wybranej grupy urządzeń,
- wszystkich urządzeń mających określony znacznik,
- wszystkich urządzeń należących do wybranego miejsca (ścieżki) w strukturze organizacyjnej.

## Definiowanie reguł

### Poprzez wybór opcji 

DO OPISANIA

### Skrypt w języku Python

DO OPISANIA

## Zmienne w komunikatach reguł

- `{target.eui}` - EUI urządzenia, którego dotyczy reeguła (jeśli dotyczy urzadzenia)
- `{target.name}` - nazwa urządzenia, którego dotyczy reeguła
- `{tag.name}` - nazwa znacznika urządzeń, którego dotyczy reguła
- `{tag.value}` - wartość znacznika urządzeń (o nazwie {tag.name}), którego dotyczy reguła
- `{device.eui}` - EUI urządzenia, dla którego reguła zadziałała
- `{device.name}` - nazwa urządzenia, dla którego reguła zadziałała
- `{var}` - nazwa pomiaru, dla którego reguła zadziałała
- `{measurement}` - nazwa pomiaru, dla którego reguła zadziałała
- `{value}` - wartość pomiaru, która spełnia regułę
- `{info}` - jeśli występuje, to służy do oddzielenie tematu wiadomości od jej treści
- `{device.owner}` - login użytkownika będącego właścicielem urządzenia
- `{device.team}` - lista loginów użytkowników wchodzących w skład zespołu urządzenia
- `{device.admins}` - lista loginów użytkowników będących administratoramiurządzenia

Przykład zastosowana w komunikacie:
```javascript
To jest temat powiadomienia{info}Uwaga! Wartość {value} parametru {measurement} dla urządzenia
{device.name} ({device.eui}) jest powyżej docelowej.

```
