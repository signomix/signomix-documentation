# Użycie kodu własnościowego

W kodzie open-source platformy Signomix znajdują się odwołania do klas Java z części niedostępnej (własnościowej).
Brak wspomnianych klas w skompilowanym kodzie powoduje wyłączenie określonych funkcjonalności.

Ten dokument opisuje sposób wykorzystania kodu własnościowego - jeżeli jest on dostępny dla osoby budującej platformę.

## Konfiguracja środowiska developerskiego

Kod niedostępny w wersji open-source jest w dodatkowej bibliotece `signomix-extensions`.
Biblioteka może być użyta w wybranych mikroserwisach poprzez zadeklarowanie zależności w `pom.xml` wybranego mikroserwisu (patrz: `signomix-reports`,`signomix-ta-account`):

```xml
<dependency>
      <groupId>com.signomix</groupId>
      <artifactId>signomix-extensions</artifactId>
      <version>1.0.1</version>
</dependency>
```

Biblioteka MUSI być budowana (np. przez skrypt `build-images.sh` w związku z czym odpowiednie repozytorium należy pobrać z GitHub. Wersja open-source tej biblioteki (konieczna, żeby platforma się budowała) jest pobierana przez skrypt `init-dev-environment.sh`.

W przypadku budowania wersji platformy z kodem własnościowym należy po uruchomieniu `init-dev-environment.sh` wykonać kroki:

1. Usunąć utworzony folder `signomix-extensions`.
2. Pobrać kod biblioteki z właściwego repozytorium do folderu `signomix-extensions` - poniżej przykładowe wywołanie.

```shell
git clone https://github.com/some-account/my-signomix-extensions.git signomix-extensions
```

## Użycie klas własnościowych w kodzie

Przykład użycia klasy rozszerzenia w kodzie:

```java
import com.signomix.common.proprietary.*;

// ...

try{
    AccountTypesIface accountTypes = (AccountTypesIface)ExtensionConfig.getExtension("com.signomix.proprietary.account.AccountTypes");
    if(null != accountTypes{
        // use extension instance
    }
}catch(Exception e){
    // handle exception
}
```