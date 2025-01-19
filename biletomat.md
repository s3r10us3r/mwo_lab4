# Historyjki

- **Jako biletomat**, chcę automatycznie aktualizować listę dostępnych biletów i ich cen, aby zapewnić zgodność z polityką przewoźnika.
- **Jako biletomat**, chcę rejestrować wszystkie transakcje i wysyłać raporty do systemu centralnego, aby umożliwić monitoring i kontrolę operacji.
- **Jako biletomat**, chcę posiadać czytelny ekran dotykowy, aby użytkownik mógł
łatwo nawigować po interfejsie.
- **Jako biletomat**, chcę być wyposażony w różne metody płatności (terminal kart,
czytnik gotówki, NFC), aby obsługiwać różnorodne transakcje.
- **Jako biletomat**, chcę wydawać resztę w gotówce, jeśli użytkownik zapłaci
nadmiarowo, aby transakcja była zgodna z oczekiwaniami.

# Przypadki użycia
```mermaid
flowchart TD
    A[Biletomat] --> B@{shape: stadium, label: "Wyświetlenie dostępnych biletów"}
    B --> C@{shape: stadium, label: "Pobranie listy biletów"}
    C --> D@{shape: stadium, label: "Wyświetlenie biletów"}
    D --> E@{shape: stadium, label: "Oczekiwanie na wybór użytkownika"}
    E -.includes.-> F@{shape: stadium, label: "Pobranie listy dostępnych biletów"}
    E -.extends.-> G@{shape: stadium, label: "Ostrzeżenie o braku danych"}
```
