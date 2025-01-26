# Historyjki

- **Jako biletomat**, chcę automatycznie aktualizować listę dostępnych biletów i ich cen, aby zapewnić zgodność z polityką przewoźnika.
- **Jako biletomat**, chcę rejestrować wszystkie transakcje i wysyłać raporty do systemu centralnego, aby umożliwić monitoring i kontrolę operacji.
- **Jako biletomat**, chcę posiadać czytelny ekran dotykowy, aby użytkownik mógł
łatwo nawigować po interfejsie.
- **Jako biletomat**, chcę być wyposażony w różne metody płatności (terminal kart,
czytnik gotówki, NFC), aby obsługiwać różnorodne transakcje.
- **Jako biletomat**, chcę wydawać resztę w gotówce, jeśli użytkownik zapłaci
nadmiarowo, aby transakcja była zgodna z oczekiwaniami.


## DIAGRAMY PRZYPADKÓW UŻYCIA
### WYŚWIETLENIE DOSTĘPNYCH BILETÓW
```mermaid
flowchart TD
    A[Biletomat] --> B@{shape: stadium, label: "Wyświetlenie dostępnych biletów"}
    B --> H@{shape: stadium, label: "Uruchomienie ekranu powitalnego"}
    H --> C@{shape: stadium, label: "Pobranie listy biletów"}
    C --> D@{shape: stadium, label: "Wyświetlenie biletów"}
    D --> E@{shape: stadium, label: "Oczekiwanie na wybór użytkownika"}
    C -.includes.-> F@{shape: stadium, label: "Pobranie listy dostępnych biletów"}
    C -.extends.-> G@{shape: stadium, label: "Ostrzeżenie o braku danych"}
```

### REALIZACJA PŁATNOŚCI
```mermaid
flowchart TD
    Biletomat["Biletomat"] --> InicjowaniePłatności(["Inicjowanie płatności"])
    InicjowaniePłatności --> PrzesłanieDanychTranzakcji(["Przesłanie danych tranzakcji"])
    PrzesłanieDanychTranzakcji --> OczekiwanienaOpdowiedz(["Oczekiwanie na Opdowiedz"])
    OczekiwanienaOpdowiedz --> Powtwierdzenie(["Potwierdzenie płatności"])
    OczekiwanienaOpdowiedz -- include --> ObsługaBłedóPłatności(["Obsługa błędów płatności"])
    InicjowaniePłatności -- include --> Anulownie(["Anulownie tranzakcji"])
    Obsługa(["Obsługa alternatywnych metod tranzakcji"]) -- extend --> InicjowaniePłatności
```

### OBSŁUGA WYBORU JĘZYKA
```mermaid
flowchart TD
   A1[Biletomat] --> B1@{shape: stadium, label: "Obsługa wyboru języka"}
   B1 -.Includes.-> C1@{shape: stadium, label: "Wyswietlenie opcji językowych"}
   C1 --> D1@{shape: stadium, label: "Rejestracja wyboru języka"}
   D1 --> E1@{shape: stadium, label: "Dostosowanie Interfejsu"}
   H1@{shape: stadium, label: "Powrót do języka domyślnego"} -.Extends.-> D1 
```
### WYŚWIETLENIE PODSUMOWANIA TRANZAKCJI
```
flowchart TD
    Gromadzeniedanychotransakcj(["Gromadzenie danych o transakcji"]) -. include .-> WyświetleniePodsumowania(["Wyświetlenie podsumowania"])
    WyświetleniePodsumowania --> OczekiwanienaDecyzję(["Oczekiwanie na decyzję użytkownika"])
    Biletomat["Biletomat"] -->  Gromadzeniedanychotransakcj(["Gromadzenie danych o transakcji"])
    Obsługaanulowania(["Obsługa anulowania"]) -. extend .->Gromadzeniedanychotransakcj & WyświetleniePodsumowania & OczekiwanienaDecyzję
```
## Wspólny diagram przypadków użycia
```mermaid
flowchart TD
    Gromadzeniedanychotransakcj(["Gromadzenie danych o transakcji"]) -. include .-> WyświetleniePodsumowania(["Wyświetlenie podsumowania"])
    WyświetleniePodsumowania --> OczekiwanienaDecyzję(["Oczekiwanie na decyzję użytkownika"])
    A -->  Gromadzeniedanychotransakcj(["Gromadzenie danych o transakcji"])
    Obsługaanulowania(["Obsługa anulowania"]) -. extend .->Gromadzeniedanychotransakcj & WyświetleniePodsumowania & OczekiwanienaDecyzję



    A[Biletomat] --> B@{shape: stadium, label: "Wyświetlenie dostępnych biletów"}
    B --> H@{shape: stadium, label: "Uruchomienie ekranu powitalnego"}
    H --> C@{shape: stadium, label: "Pobranie listy biletów"}
    C --> D@{shape: stadium, label: "Wyświetlenie biletów"}
    D --> E@{shape: stadium, label: "Oczekiwanie na wybór użytkownika"}
    C -.includes.-> F@{shape: stadium, label: "Pobranie listy dostępnych biletów"}
    C -.extends.-> G@{shape: stadium, label: "Ostrzeżenie o braku danych"}


    A --> InicjowaniePłatności(["Inicjowanie płatności"])
    InicjowaniePłatności --> PrzesłanieDanychTranzakcji(["Przesłanie danych tranzakcji"])
    PrzesłanieDanychTranzakcji --> OczekiwanienaOpdowiedz(["Oczekiwanie na Opdowiedz"])
    OczekiwanienaOpdowiedz --> Powtwierdzenie(["Potwierdzenie płatności"])
    OczekiwanienaOpdowiedz -. include .-> ObsługaBłedóPłatności(["Obsługa błędów płatności"])
    InicjowaniePłatności -. include .-> Anulownie(["Anulownie tranzakcji"])
    Obsługa(["Obsługa alternatywnych metod tranzakcji"]) -. extend .-> PrzesłanieDanychTranzakcji

   A --> B1@{shape: stadium, label: "Obsługa wyboru języka"}
   B1 -.Includes.-> C1@{shape: stadium, label: "Wyswietlenie opcji językowych"}
   C1 --> D1@{shape: stadium, label: "Rejestracja wyboru języka"}
   D1 --> E1@{shape: stadium, label: "Dostosowanie Interfejsu"}
   H1@{shape: stadium, label: "Powrót do języka domyślnego"} -.Extends.-> D1  
```

### Diagram sekwencji WYŚWIETLENIE DOSTĘPNYCH BILETÓW
```mermaid
    sequenceDiagram
        participant Użytkownik as Użytkownik
        participant Biletomat as Biletomat
        participant System as System biletowy

        Użytkownik->>Biletomat: Rozpoczęcie interakcji
        Biletomat->>Użytkownik: Uruchomienie ekranu powitalnego
        Biletomat->>System: Żądanie listy dostępnych biletów
        System->>System: Sprawdzenie aktualnych taryf (Include)
        System-->>Biletomat: Przesłanie listy biletów
        Biletomat->>Użytkownik: Wyświetlenie kategorii biletów
        Użytkownik->>Biletomat: Wybór kategorii biletu
        Biletomat->>Użytkownik: Wyświetlenie szczegółów biletów
        Użytkownik->>Biletomat: Wybór biletu
        alt Awaria sieci
            Biletomat->>Użytkownik: Ostrzeżenie o braku danych (Extend)
        end
```
### Diagram sekwencji OBSŁUGA WYBORU JĘZYKA
```mermaid
sequenceDiagram
    participant Użytkownik as Użytkownik
    participant Biletomat as Biletomat

    Użytkownik->>Biletomat: Rozpoczęcie interakcji
    Biletomat->>Użytkownik: Wyświetlenie opcji językowych 
    Użytkownik->>Biletomat: Wybór preferowanego języka
    Biletomat->>Biletomat: Rejestracja wyboru języka
    Biletomat->>Biletomat: Dostosowanie interfejsu do wybranego języka
    alt Brak aktywności użytkownika
        Biletomat->>Biletomat: Powrót do języka domyślnego (Extend)
    else Anulowanie procesu
        Użytkownik->>Biletomat: Anulowanie transakcji (Include)
    end

```