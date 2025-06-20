# Zarządzanie dokumentacją organizacji

Dokumentacja organizacji jest przechowywana w repozytorium GitHub utworzonym dla danej organizacji i dostępnym dla wskazanych użytkowników.

Dokumentacja jest serwowana przez działający w ramach platformy Signomix serwis Cricket HCMS i jest dostępna dla członków organizacji poprzez opcję `Pomoc` w menu webaplikacji Signomiksa, widoczną po zalogowaniu się na swoje konto.

## Udostępnianie dokumentacji

Aby udostępnić dokumentację organizacji, należy utworzyć repozytorium GitHub i dodać do niego pliki dokumentacji. Repozytorium powinno być publiczne lub dostępne dla użytkownika, którzy będzie konfigurował dokumentację organizacji na serwerze.

1. Klonowanie repozytorium na serwerze, na którym działa Signomix.

Jeśli folderem zawierającym dokumentacje organizacyjne jest `~/volumes/organization-docs`, a identyfikatorem organizacji `Demo` jest `2`, to repozytorium można sklonować poleceniem:

```bash
cd ~/volumes/organization-docs
git clone https://github.com/signomix/signomix-demo-documentation.git 2
```
Polecenie to utworzy folder `~/volumes/organization-docs/2`, w którym będą przechowywane pliki dokumentacji organizacji `Demo`.

2. Konfiguracja obsługi dokumentacji `Demo` przez serwis Cricket HCMS.

