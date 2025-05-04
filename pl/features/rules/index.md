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

Reguła może być aktywna lub nie.

Regułę analizy danych przychodzących definiuje się dla:
- urządzenia o wybranym identyfikatorze (EUI),
- grupy,
- urządzeń oznaczonych tagiem o wybranej nazwie i wartości.

Można ograniczyć analizę do danych nie starszych niż określona liczba minut.

Przy analizie zmian wartości uwzględniana jest histereza.

W przypadku, kiedy dane spełniają warunki reguły system generuje powiadomienie o wybranym poziomie ważności:
- Info
- Warning
- Alert 
- Critical
- Emergency

Powiadomienie jest kierowane do wybranej listy użytkowników.
Opcjonalnie, w przypadku gdy reguła przestanie być spełniana (wartości danych wrócą do oczekiwanego zakresu), system generuje powiadomienie kierowane do podanej listy użytkowników.

Warunki analizy danych definiowane są poprzez:
- wybranie opcji w formularzu,
- zdefiniowanie skryptu analizującego dane.

### Wybór opcji 

Jeżeli na formularzu znacznik `skrypt` nie jest zaznaczony, to warunki można zdefiniować poprzez wypełnienie pojawiających się pól formularza i określenie:
- nazwy analizowanego pomiaru,
- warunku porównywania (mniejsze, większe, równe, różne),
- wartości z którą należy porównać.

Można zdefiniować kilka takich warunków.

### Skrypt w języku Python

Definiując warunki przy użyciu skryptu można sprawdzić więcej zależności niż wybierając opcje z formularza. Na przykład porównać zesobą różne pomiary.

Skrypt musi definiować funkcję `checkRule()` zwracającą wynik poprzez wywołanie funkcji `conditionsNotMet()` lub `conditionsMet()`.

Przykład:
```python
def checkRule():
    v1 = getValue("temperature1")
    v2 = getValue("temperature2")
    if v1 is None or v2 is None:
        return conditionsNotMet()
    if v2 - v1 > 10:
        return conditionsMet("temperature2",v2)
    return conditionsNotMet()
```

## Zmienne w komunikatach reguł

Przy tworzeniu treści komunikatów można użyć następujących zmiennych:

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
