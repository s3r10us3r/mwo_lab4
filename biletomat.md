
- **Jako biletomat**, chcę automatycznie aktualizować listę dostępnych biletów i ich cen, aby zapewnić zgodność z polityką przewoźnika.
- **Jako biletomat**, chcę rejestrować wszystkie transakcje i wysyłać raporty do systemu centralnego, aby umożliwić monitoring i kontrolę operacji.
- **Jako biletomat**, chcę posiadać czytelny ekran dotykowy, aby użytkownik mógł
łatwo nawigować po interfejsie.
- **Jako biletomat**, chcę być wyposażony w różne metody płatności (terminal kart,
czytnik gotówki, NFC), aby obsługiwać różnorodne transakcje.
- **Jako biletomat**, chcę wydawać resztę w gotówce, jeśli użytkownik zapłaci
nadmiarowo, aby transakcja była zgodna z oczekiwaniami.

## DIAGRAMY PRZYPADKÓW UŻYCIA
### REALIZACJA PŁATNOŚCI
```MERMAID
flowchart TD
    Biletomat["Biletomat"] --> InicjowaniePłatności(["Inicjowanie płatności"])
    InicjowaniePłatności --> PrzesłanieDanychTranzakcji(["Przesłanie danych tranzakcji"])
    PrzesłanieDanychTranzakcji --> OczekiwanienaOpdowiedz(["Oczekiwanie na Opdowiedz"])
    OczekiwanienaOpdowiedz --> Powtwierdzenie(["Potwierdzenie płatności"])
    OczekiwanienaOpdowiedz -- include --> ObsługaBłedóPłatności(["Obsługa błędów płatności"])
    InicjowaniePłatności -- include --> Anulownie(["Anulownie tranzakcji"])
    Obsługa(["Obsługa alternatywnych metod tranzakcji"]) -- extend --> PrzesłanieDanychTranzakcji