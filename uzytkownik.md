
- **Jako użytkownik**, chcę szybko wybierać rodzaj biletu, aby zminimalizować czas spędzony przy biletomacie.
- **Jako użytkownik**, chcę mieć możliwość wyboru języka, aby móc korzystać z biletomatu bez względu na znajomość języka lokalnego.
- **Jako użytkownik**, chcę sprawdzić poprawnośc transakcji przed jej finalizacją, aby uniknać pomyłek.
- **Jako użytkownik**, chcę otrzymać potwierdzenie zakupu (np. wydruk biletu lub elektroniczny bilet), aby móc korzystać z transportu zgodnie z przepisami.
- **Jako użytkownik**, chcę płacić za bilet kartą, gotówką lub telefonem, aby mieć
większą elastyczność w wyborze metody płatności.
- **Jako użytkownik**, chcę otrzymać wyraźne instrukcje na ekranie, aby wiedzieć,
jak dokonać zakupu krok po kroku.
- **Jako użytkownik**, chcę widzieć czas pozostały na decyzję (np. wyświetlany
licznik czasu), aby móc szybko podjąć działanie.

## DIAGRAMY PRZYPADKÓW UŻYCIA


### SZYBKI WYBÓR RODZAJU BILETU
```mermaid
flowchart TD
    Uzytkownik["Użytkownik"] --> PodchodziDoBiletomatu(["Rozpoczęcie interakcji"])
    PodchodziDoBiletomatu --> WybieraKategorieBiletu(["Wybór kategorii"])
    WybieraKategorieBiletu --> WybieraBilet(["Wybiera bilet"])
    WybieraBilet --> WyświetleniePodsumowania(["Wyświetlenie podsumowania"])
    WybieraKategorieBiletu -- include --> Anulowanie(["Anulowanie"])
    WybieraBilet -- include --> Anulowanie & SprawdzenieBiletów(["Sprawdzenie biletów"])
    PotwierdzaBilet(["Potwierdza wybóru"]) -- include --> Anulowanie
    Wyświetleniepodpowiedzi(["Wyświetlenie podpowiedzi"]) -- extend --> WybieraKategorieBiletu & WybieraBilet
    WyświetleniePodsumowania --> PotwierdzaBilet
    PodchodziDoBiletomatu -- include --> Anulowanie
    WyświetleniePodsumowania -- include --> Anulowanie
```
### WYBÓR JĘZTKA
```mermaid
flowchart TD
    Uzytkownik["Użytkownik"] --> PodchodziDoBiletomatu(["Rozpoczęcie interakcji"])
    PodchodziDoBiletomatu --> WyswietlenieOpcjiJezyka(["Wyświetlenie opcji języka"])
    WyswietlenieOpcjiJezyka --> WybórJęzyka(["Wybór języka"])
    WybórJęzyka --> DostosowanieInterfejsu(["Dostosowanie Interfejsu"])
    Anulowanietransakcji(["Anulowanie transakcji"]) -- extend --> WybórJęzyka & DostosowanieInterfejsu & WyswietlenieOpcjiJezyka
    PodchodziDoBiletomatu -- include --> DomyslnyJezyk(["Domyślny język"])
    WyswietlenieOpcjiJezyka -- extend --> ListaPop(["Lista popularnych języków"])
```

### PŁATNOŚĆ ZA BILET
```mermaid
flowchart TD
    Uzytkownik --- B@{shape: stadium, label: "Wybór metody płatności"}
    B --> C@{shape: stadium, label: "Weryfikacja metody płatności"}
    C --> D@{shape: stadium, label: "Realizacja płatności"}
    D --> E@{shape: stadium, label: "Potwierdzenie transakcji"}
    F@{shape: stadium, label: "Anulowanie transakcji"}
    B -.includes.-> F
    C -.includes.-> F
    D -.includes.-> F
    C -.extends.-> G@{shape: stadium, label: "Obsługa błędów płatności"}
```

### SPRAWDZENIE POPRAWNOŚCI TRANZAKCJI
```mermaid
flowchart TD
   A[Użytkownik] --> B@{shape: stadium, label: "Sprawdzenie poprawności transakcji"}
   B --> E@{shape: stadium, label: "Wybór biletu i płatności"}
   E --> C@{shape: stadium, label: "Wyświetlenie podsumowania"}
   C --> D@{shape: stadium, label: "Potwierdzenie lub cofnięcie"}
   
   

   F@{shape: stadium, label: "Anulowanie transakcji"}
   G@{shape: stadium, label: "Ostrzeżenie o błędzie"}

   G -.Extends.-> B
   B -.Includes.-> F
   C -.Includes.-> F
   E -.Includes.-> F
   D -.Includes.-> F
```

### WSPÓLNY DIAGRAM
```mermaid
---
config:
  layout: elk
---
flowchart TD
    Uzytkownik["Użytkownik"] --> PodchodziDoBiletomatu(["Rozpoczęcie interakcji"]) & B2(["Sprawdzenie poprawności transakcji"])
    PodchodziDoBiletomatu --> WybieraKategorieBiletu(["Wybór kategorii"]) & WyswietlenieOpcjiJezyka(["Wyświetlenie opcji języka"])
    WybieraKategorieBiletu --> WybieraBilet(["Wybiera bilet"])
    WybieraBilet --> WyświetleniePodsumowania(["Wyświetlenie podsumowania"])
    WybieraKategorieBiletu -. include .-> Anulowanie(["Anulowanie"])
    WybieraBilet -. include .-> Anulowanie & SprawdzenieBiletów(["Sprawdzenie biletów"])
    PotwierdzaBilet(["Potwierdza wybóru"]) -. include .-> Anulowanie
    Wyświetleniepodpowiedzi(["Wyświetlenie podpowiedzi"]) -- extend --> WybieraKategorieBiletu & WybieraBilet
    WyświetleniePodsumowania --> PotwierdzaBilet
    PodchodziDoBiletomatu -. include .-> Anulowanie & DomyslnyJezyk(["Domyślny język"])
    WyświetleniePodsumowania -. include .-> Anulowanie
    WyswietlenieOpcjiJezyka --> WybórJęzyka(["Wybór języka"])
    WybórJęzyka --> DostosowanieInterfejsu(["Dostosowanie Interfejsu"])
    Anulowanietransakcji(["Anulowanie transakcji"]) -. extend .-> WybórJęzyka & DostosowanieInterfejsu & WyswietlenieOpcjiJezyka
    WyswietlenieOpcjiJezyka -. extend .-> ListaPop(["Lista popularnych języków"])
    PotwierdzaBilet --> C(["Weryfikacja metody płatności"])
    C --> D(["Realizacja płatności"])
    D --> E(["Potwierdzenie transakcji"])
    B["B"] -. includes .-> F(["Anulowanie transakcji"])
    C -. includes .-> F
    D -. includes .-> F
    C -. extends .-> G(["Obsługa błędów płatności"])
    B2 --> E2(["Wybór biletu i płatności"])
    E2 --> C2(["Wyświetlenie podsumowania"])
    C2 --> D2(["Potwierdzenie lub cofnięcie"])
    G2(["Ostrzeżenie o błędzie"]) -. Extends .-> B2
    B2 -. Includes .-> F2(["Anulowanie transakcji"])
    C2 -. Includes .-> F2
    E2 -. Includes .-> F2
    D2 -. Includes .-> F2
```


### Diagram sekwencji WYBÓR JĘZYKA
```mermaid
sequenceDiagram
    participant U as Użytkownik
    participant B as Biletomat

    U ->> B: Rozpoczęcie interakcji
    B ->> B: Domyślny język

    B ->> U: Wyświetlenie opcji języka
    alt Lista popularnych języków
        B ->> U: Wyświetlenie listy popularnych języków
    end

    U ->> B: Wybór języka
    alt Anulowanie transakcji
        U ->> B: Anulowanie
    else
        B ->> U: Dostosowanie interfejsu
        alt Anulowanie transakcji
            U ->> B: Anulowanie
        else
            B ->> B: Zakończenie
        end
    end
```

### Diagram sekwencji SZYBKI WYBÓR RODZAJU BILETU
```mermaid
sequenceDiagram
    actor U as Użytkownik
    participant I as Biletomat
    participant S as Serwer
    
    alt Anulowanie
    U ->> I: Wybiera opcję anuluj
    I -->> U: Wyświetla ekran początkowy
    else
    U ->> I: Wybiera opcję szybkiego wyboru biletu
    I ->> S: Wysyła zapytanie o dostępne kategorie
    S -->> I: Dostępne kategorie
    I -->> U: Wyświetla ekran wyboru kategorii
    alt wyświetlenie podpowiedzi
    U ->> I: Nie odpowiada
    I -->> U: Wyświetla podpowiedź
    U ->> I: Wybiera przycisk zamknięcia podpowiedzi
    I --> U: Zamyka podpowiedź
    else
    U ->> I: Wybiera kategorię
    I ->> S: Wysyła zapytanie o dostępne bilety
    S -->> I: Lista dostępnych biletów
    I -->> U: Wyświetla ekran wyboru biletu
    U ->> I: Wybiera bilet
    I ->> S: Wysyła zapytanie o sprawdzenie biletów
    S -->> I: Akceptacja biletów
    I -->> U: Wyświetla ekran podsumowania
    U ->> I: Potwierdza wybór
    I -->> U: 
    end
    end
```
