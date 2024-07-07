# Kontrolka typu `LED`

Wyświetla ikonę, której wygląd i kolor są uzależnione od zdefiniowanej reguły alertu dla powiązanego z nią pomiaru.

Poniższa ilustracja przedstawia wygląd trzech kontrolek LED kolejno dla: braku ostrzeżenia, ostrzeżenia oraz alarmu.

<img class="border rounded shadow mt-1 mb-3" width="30%" src="/api/file?path=signomix-documentation/features/dashboards/led1.png">

## Konfigurowanie

Konfigurując kontrolkę `LED' należy wypełnić pola:

- **EUI** - identyfikator źródła danych
- **Nazwy pomiarów** - nazwa wybranego pomiaru przesyłanego przez wybrane źródło danych (np. temperature, humidity itp.) - **jedna nazwa**
- **Reguła alarmu** - reguła uzależniająca rodzaj ikony oraz jej kolor od ostatniej wartości pomiaru
- **Ikony** - pozostawienie tego pola pustego powoduje, że zostanie zastosowany domyślny zestaw ikon

<img class="border rounded shadow mt-1 mb-3" width="30%" src="/api/file?path=signomix-documentation/features/dashboards/widget1.png"><br>

<img class="border rounded shadow mt-1 mb-3" width="30%" src="/api/file?path=signomix-documentation/features/dashboards/widget2.png">

## Reguła alarmu

Reguła określa jaki zakres wartości pomiaru będzie oznaczać wartość alarmową, a jaki ostrzeżenie.

Składnia reguły:<br>
<pre class="boredr shadow p-2 bg-secondary-subtle">
reguła: {alertCondition}[:{warningConditon}][@variableName][#maxDelay]
alertCondition|warningCondition: [variableName]{comparator1}{value}[[variableName]{comparator1}{value}]
comparator: >|<
</pre>
gdzie:
- variableName - nazwa pomiaru
- value - wartość
- maxDelay - maksymalny czas od ostatniego pomiaru do chwili obecnej - starsze dane nie będą uwzględniane i w przypadku braku danych najnowszych stan kontrolki będzie nieustalony
- jeśli alertCondition lub warningCondition zawiera warunki dla 2 komparatorów, to zachodzi między nimi warunek logiczny OR 

Przykłady definicji:
<pre class="boredr shadow p-2  bg-secondary-subtle">
x<-10>40:x<0>30
<-10>40:<0>30
<-10>40:<0>30@temperature
<-10>40:<0>30@temperature#1h
x<-10>40:x<0>30#2m
</pre>

## Deklarowanie zestawu ikon

Standardowy zestaw ikon można zmienić poprzez zadeklarowanie ich w polu **Ikony**. Obsługiwane są ikony dostępne w projekcie https://icons.getbootstrap.com/<br>
Nazwy ikon muszą być oddzielone znakiem dwukropka `:`.

Przykład wybranych ikon oraz uzyskany wygląd poniżej.

<pre class="boredr shadow p-2  bg-secondary-subtle">
bi-arrow-up-square-fill:bi-arrow-right-square-fill:bi-arrow-down-square-fill
</pre>

<img class="border rounded shadow mt-1 mb-3" width="30%" src="/api/file?path=signomix-documentation/features/dashboards/led2.png">

