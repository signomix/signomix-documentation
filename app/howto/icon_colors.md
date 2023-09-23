# Własne kolory ikon na kontrolkach pulpitu

Kolory ikon prezentowanych na kontrolkach [symbol](/app/dashboards/widget-symbol.md) oraz [sygnalizator](/app/dashboards/widget-led.md) mogą być uzależnione od prezentowanej wartości pomiaru.
Konfigurując te kontrolki można podać zakresy wartości odpowiadające:
- wartościom normalnym - kolor zielony
- wartościom ostrzegawczym - kolor żółty
- wartościom alarmowym - kolor czerwony

Zmiana powyższego zestawu kolorów jest możliwa poprzez zmianę konfiguracji kontrolki.


```json
{
    "colors": [
		"text-success",
		"text-warning",
		"text-danger",
		"text-muted",
		"text-muted"
	]
}
```