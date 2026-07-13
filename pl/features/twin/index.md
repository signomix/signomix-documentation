# Cyfrowy bliźniak

Cyfrowy bliźniak jest cyfrowym odwzorowaniem fizycznego obiektu lub urządzenia. Jego parametry mogą być rejestrowane przez powiązany z nim zestaw czujników. Signomix pozwala na zapisanie wartości tych parametrów jako parametry cyfrowego bliźniaka. Dzięki temu można obserwować stan obiektu w spójny sposób - znacznie łatwiej niż poprzez pobieranie danych oddzielnie z każdego powiązanego czujnika.

## Definiowanie cyfrowego bliźniaka

## Przesyłane danych

Dane odbierane przez mikroserwis `signomix-ta-receiver` ze źródła danych (urządzenia) są po przetworzeniu przesyłane do brokera komunikatów i odbierane przez mikroserwis `signomix-collector`.

Mikroserwis `signomix-collector` przypisuje źródło danych (na podstawie jego `EUI`) do bliźniaka i zapisuje odebrane dane w bazie danych tego bliźniaka. Za mapowanie eui na eui bliźniaka i nazw danych na nazwy danych bliźniaka odpowiada klasa **TwinMapper**.

## Raporty

Dedykowany raport: `com.signomix.reports.pre.TwinsReport`