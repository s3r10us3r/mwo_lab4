
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

### Płatność za bilet
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

### Wspólny diagram
```mermaid
flowchart TD
    %% --- SZYBKI WYBÓR RODZAJU BILETU ---
    Uzytkownik["Użytkownik"] --> PodchodziDoBiletomatu(["Rozpoczęcie interakcji"])
    PodchodziDoBiletomatu --> WybieraKategorieBiletu(["Wybór kategorii"])
    WybieraKategorieBiletu --> WybieraBilet(["Wybiera bilet"])
    WybieraBilet --> WyświetleniePodsumowania(["Wyświetlenie podsumowania"])
    WybieraKategorieBiletu -- include --> Anulowanie(["Anulowanie"])
    WybieraBilet -- include --> Anulowanie & SprawdzenieBiletów(["Sprawdzenie biletów"])
    WyświetleniePodsumowania --> PotwierdzaBilet(["Potwierdza wybór"])
    PodchodziDoBiletomatu -- include --> Anulowanie
    WyświetleniePodsumowania -- include --> Anulowanie

    %% Wyświetlanie dodatkowych podpowiedzi (zależne od rozszerzenia)
    WyświetleniePodpowiedzi(["Wyświetlenie podpowiedzi"]) -- extend --> WybieraKategorieBiletu
    WyświetleniePodpowiedzi -- extend --> WybieraBilet

    PotwierdzaBilet -- include --> Anulowanie

    %% --- PRZEJŚCIE DO PŁATNOŚCI ZA BILET ---
    Uzytkownik --> B@{shape: stadium, label: "Wybór metody płatności"}
    B --> C@{shape: stadium, label: "Weryfikacja metody płatności"}
    C --> D@{shape: stadium, label: "Realizacja płatności"}
    D --> E@{shape: stadium, label: "Potwierdzenie transakcji"}
    F@{shape: stadium, label: "Anulowanie transakcji"}

    %% Uwzględnienie Anulowania i Obsługi błędów w procesie płatności
    B -.includes.-> F
    C -.includes.-> F
    D -.includes.-> F
    C -.extends.-> G@{shape: stadium, label: "Obsługa błędów płatności"}git 
```
