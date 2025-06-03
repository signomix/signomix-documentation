# Budowa i uruchamianie Signomiksa lokalnie

We wszystkich dokumentach odnoszących się do środowiska developerskiego przyjmuje się, że wszystkie repozytoria Git są sklonowane do tego wspólnego folderu <WORKSPACE>, np. /home/developer1/workspace.

> UWAGA!<br>
> Wszystkie przykłady komend i plików konfiguracyjnych są podane dla Linuksa (dystrybucja Ubuntu). W przypadku innego systemu operacyjnego podane przykłady należy odpowiednio zmodyfikować.
><br> Założono, że wszystkie repozytoria Git są sklonowane do tego wspólnego folderu `<WORKSPACE>`, np. /home/developer1/workspace.

## Wymagane oprogramowanie

### Java 17 JDK

Java jest wymagana do kompilacji kodu. Przykładowy opis instalacji: https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/install-java-jdk-17-on-ubuntu-22-04.html?utm_content=cmp-true

```shell
sudo apt update
sudo apt install -y openjdk-17-jdk
java -version
```
Strona domowa: https://openjdk.org/

### Git

```shell
sudo apt install git
git –version
```

Strona domowa:  https://git-scm.com/

### Maven

```shell
sudo apt install maven
mvn --version
```

Strona domowa: https://maven.apache.org/

### Quarkus

Opcjonalnie - przydatny do inicjowania nowych serwisów wykorzystujących framework Quarkus

```shell
curl -Ls https://sh.jbang.dev | bash -s - trust add https://repo1.maven.org/maven2/io/quarkus/quarkus-cli/
curl -Ls https://sh.jbang.dev | bash -s - app install --fresh --force quarkus@quarkusio
```

Strona domowa: https://quarkus.io/get-started/

### Docker

Instalację przeprowadzić zgodnie z: https://docs.docker.com/engine/install/ubuntu/ <br>
Czynności poinstalacyjne: https://docs.docker.com/engine/install/linux-postinstall/

Po poprawnym zainstalowaniu można sprawdzić czy wszystko działa uruchamiając kolejno testowy obraz hello-world, a następnie docker compose:

```shell
# uruchomienie hello-world
docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

# sprawdzenie jaka wersja Docker Compose
docker compose version
Docker Compose version v2.26.1

```

## Przygotowanie środowiska

### Folder roboczy

W tym dokumencie nazwa folder roboczy oznacza podfolder folderu domowego użytkownika. Do folderu roboczego będą sklonowane wszystkie wymagane repozytoria platformy Signomix. We wszystkich przykładowych komendach zawartych w  tym dokumencie oznaczenie `<WORKSPACE>` należy zamienić na wybraną nazwę.

```shell
# utworzenie przykładowego folderu roboczego w folderze domowym użytkownika
mkdir ~/workspace
```

### Adresy subdomen

Zmodyfikować zawartość pliku `/etc/hosts` dodając poniższe linie:

```any
# file /etc/hosts
127.0.0.1 localhost
127.0.0.1 app.localhost
127.0.0.1 www.localhost
127.0.0.1 view.localhost
127.0.0.1 cloud.localhost
127.0.0.1 documentation.localhost
127.0.0.1 telemetry.localhost
127.0.0.1 q1.localhost
```

### Klonowanie repozytoriów

Jeżeli wcześniej nie zostało to zrobione, należy sklonować wszystkie wymagane repozytoria do folderu roboczego `<WORKSPACE>`. Ułatwia to skrypt init-dev-environment.sh w repozytorium signomix. Skrypt ten klonuje wymagane repozytoria oraz tworzy foldery, które muszą być montowane jako volumeny dla kontenerów dockerowych.

```shell
cd ~/<WORKSPACE>
git clone https://github.com/signomix/signomix
cd signomix
sh init-dev-environment.sh
```

### Zarządzanie sekretami konfiguracji

Niektóre z parametrów konfiguracyjnych nie powinny być przechowywane w publicznie dostępnych repozytoriach. Dotyczy to na przykład loginów, haseł lub tokenów API. Signomix wykorzystuje dwa mechanizmy Docker Compose w celu rozwiązania tego problemu:

- Docker Compose Secrets - https://docs.docker.com/compose/how-tos/use-secrets/
- atrybut `env_file` Docker Compose - https://docs.docker.com/compose/how-tos/environment-variables/set-environment-variables/#use-the-env_file-attribute

Skrypt `init-dev-environment.sh` kopiuje zestaw plików z ustawieniami do katalogu `.secrets` w katalogu domowym użytkownika (patrz: `init-runtime-environment.sh`).

**Przed uruchomieniem Signomiksa należy przejrzeć zawartość plików w katalogu `~/.secrets` i wymienić ustawienia na własne.**
   
### Budowanie wersji developerskiej

```shell
cd ~/<WORKSPACE>/signomix
./build-images.sh
```

W przypadku, gdy nie ma lokalnych zmian w kodzie, można przed wywołaniem powyższego polecenia pobrać najnowsze wersje kodu z repozytoriów. Ułatwia to skrypt pull-repositories.sh

```shell
./pull-repositories.sh
```

### Uruchamianie wersji developerskiej

```shell
cd ~/<WORKSPACE>/signomix
./runInDevEnvironment.sh up -d
```

Uruchomiona platforma jest dostępna pod adresami:
- http://www.localhost
- http://cloud.localhost
- http://view.localhost
- http://documentation.localhost
- http://telemetry.localhost
- http://q1.localhost

Predefiniowane konta:

|Konto|Login|Hasło|
|---|---|---|
|Administrator|admin|test123
|Użytkownik|tester1|test123|


### Zatrzymywanie działającej wersji

```shell
cd ~/<WORKSPACE>/signomix
./runInDevEnvironment.sh down
```