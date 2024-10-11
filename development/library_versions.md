# Wersje współdzielonych bibliotek

Mikroserwisy składające się na platformę Signomix mogą wykorzystywać kod zawarty w dwóch współdzielonych bibliotekach: `signomix-common` oraz `signomix-extensions`.

Jeżeli mikroserwis potrzebuje tych bibliotek, to jego plik `pom.xml` musi deklarować poniższe zależności:

```xml
<dependency>
    <groupId>com.signomix</groupId>
    <artifactId>signomix-common</artifactId>
    <version>1.18.0</version>
</dependency>
<dependency>
    <groupId>com.signomix</groupId>
    <artifactId>signomix-extensions</artifactId>
    <version>1.2.0</version>
</dependency>
```

## Zarządzanie wersjami

Poszczególne mikroserwisy, których kod jest w repozytoriach GitHub może mieć deklaracje różnych wersji tych współdzielonych bibliotek. Dzieje się to dlatego, że rozwój mirkoserwisów nie zawsze jest ze sobą zsynchronizowany.

Przed przystąpieniem do budowania platformy w nowym środowisku developerskim należy sprawdzić pliki `pom.xml` wszystkich mikroserwisów i zmienić numery wersji tych bibliotek na najnowsze. ***Może to spowodować konieczność wprowadzenia modyfikacji w kodach mikroserwisów w celu dostosowania ich do najnowszych wersji bibliotek.***