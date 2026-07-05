# Metodologia — zasady działania narzędzia

## Cel

Narzędzie wykonuje **przesiew wstępny** (screening), nie audyt. Jego zadaniem jest w 60 sekund dać użytkownikowi orientacyjny sygnał: czy warto zainwestować czas w pełną, płatną analizę. Nie jest to wycena, gwarancja przyznania środków ani opinia prawna.

## Struktura logiki

### 1. Dopasowanie sektor → programy

Każdy z 8 sektorów ma przypisaną statyczną listę 2–3 kategorii programów wsparcia (`PROGRAMS` w kodzie źródłowym). Lista jest budowana ręcznie na podstawie znanych, względnie trwałych instrumentów (KPO, FEW, Dig.IT, BUR/KFS, jednorazowa amortyzacja) — **nie jest połączona z żadnym rejestrem naborów w czasie rzeczywistym.**

**Konsekwencja praktyczna:** listę programów należy przeglądać i aktualizować **nie rzadziej niż raz na kwartał**, a także każdorazowo po istotnej zmianie harmonogramu naborów (np. nowa perspektywa finansowa, nowelizacja ustawy o KSC). Nieaktualna lista to największe ryzyko wiarygodności narzędzia.

### 2. Heurystyka potencjału PLN

```
baza = wartość_bazowa(wielkość_firmy)   // mikro/małe/średnie/duże
zakres_dolny  = baza × 0,6
zakres_górny  = baza × 1,4
jeśli planowana inwestycja:
    zakres_dolny  += kwota_inwestycji × 0,15
    zakres_górny  += kwota_inwestycji × 0,35
jeśli brak historii korzystania z dotacji:
    zakres_górny  ×= 1,1   // większy niewykorzystany potencjał
```

Wartości bazowe (`SIZE_BASE`) są **szacunkiem rzędu wielkości**, nie kalibracją statystyczną — dobrane tak, by orientacyjnie odzwierciedlać typową skalę dostępnego wsparcia dla danej wielkości firmy w Polsce. Nie mają źródła regulacyjnego i są jawnie oznaczone jako `[SZACUNEK MODELOWY]`.

### 3. System etykiet epistemicznych

Każde stwierdzenie w wyniku jest opatrzone jedną z trzech etykiet:

| Etykieta | Znaczenie |
|---|---|
| **FAKT REGULACYJNY** | Istnienie programu/instrumentu jest potwierdzone (nazwa, podstawa prawna lub instytucja). Nie oznacza to gwarancji kwalifikowalności konkretnego wnioskodawcy. |
| **SZACUNEK MODELOWY** | Wartość obliczona heurystycznie (np. zakres PLN) — matematyczna konsekwencja przyjętych założeń, nie dana empiryczna. |
| **HIPOTEZA STRATEGICZNA** | Wnioskowanie wymagające weryfikacji indywidualnej (np. lokalizacja względem obszarów chronionych, klasyfikacja NIS2). |

Cel systemu: uniknięcie iluzji precyzji, którą tworzą narzędzia prezentujące szacunki jako twarde liczby. To rozróżnienie jest też sygnałem jakości dla odbiorcy — pokazuje, że narzędzie nie zgaduje w ciemno.

### 4. Flaga NIS2 / uKSC

Zaznaczenie checkboxa w §3 nie oznacza automatycznej kwalifikacji jako podmiot kluczowy/ważny. Ustawa o KSC wymaga samodzielnej klasyfikacji przez podmiot — narzędzie jedynie sygnalizuje, że **warto tę klasyfikację formalnie wykonać**, ponieważ brak samoidentyfikacji nie chroni przed odpowiedzialnością.

## Ograniczenia (jawne)

- Brak weryfikacji lokalizacji (istotne np. dla Natura 2000, programów regionalnych).
- Brak połączenia z rejestrem aktualnych naborów — terminy i stawki wymagają weryfikacji na dzień składania wniosku.
- Heurystyka PLN nie uwzględnia sytuacji finansowej firmy (zdolność do wkładu własnego, historia kredytowa) — czynników decydujących o realnej szansie sukcesu.
- Klasyfikacja sektorowa jest uproszczona do 8 kategorii; firmy wielobranżowe (PKD z kilku kategorii) mogą wymagać analizy wykraczającej poza jeden wybór.

## Rekomendowany cykl aktualizacji

| Element | Częstotliwość |
|---|---|
| Lista programów (`PROGRAMS`) | Kwartalnie |
| Wartości bazowe heurystyki (`SIZE_BASE`) | Rocznie lub po istotnej zmianie rynkowej |
| Cennik | Po każdej zmianie pozycjonowania — patrz CENNIK.md |
