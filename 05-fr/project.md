# System aukcyjny

## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny. 

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna 

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego. |

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([BR1](#br1))
3. [Kupujący](#ac2) wygrywa aukcję ([BR2](#br2))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu.
5. [Sprzedający](#ac1) przekazuje produkt Kupującemu.

**Scenariusze alternatywne:** 

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję. ([BR2](#br2))
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.


## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję
* [UC1](#uc1): Podanie ceny i danych produktu

[Kupujący](#ac2)
* ...

---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:** 

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc2"></a>
### UC2: Licytacja produktu

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Scenariusz główny:**
1. [kupujący](#ac2) zgłasza do systemu chęć zakupy produktu na aukcji.
2. System prosi o podanie kwoty za oferowany produkt.
3. [kupujący](#ac2) podaje kwotę.
4. System weryfikuje poprawność danych.
5. System informuje o zatwierdzeniu oferty i aktualizuje kwotę licytacji.
6. System informuje pozostałych [kupujący](#ac2)ch o nowej kwocie licytacji.
7. System informuje [sprzedający](#ac1) o nowej ofercie na licytacji jego produktu.
8. System po upływie określonego czasu wybiera najwyższą oferowaną kwotę.
9. System informuje [sprzedający](#ac1) o zakończeniu aukcji i jej kwocie.
10. System informuje [kupujący](#ac2) o wygraniu aukcji.
11. System pobiera środki z salda [kupujący](#ac2).
12. System przekazuje środki na saldo [sprzedający](#ac1).
13. System prosi [kupujący](#ac2) o dane do wysyłki produktu.
14. [kupujący](#ac2) podaje dane do wysyłki produktu.
15. System wysyła dane do wysyłki produktu dla [sprzedający](#ac1).
16. [sprzedający](#ac1) wysyła produkt.
17. System zamyka aukcję.

**Scenariusze alternatywne:** 

1.A. Żaden kupujący nie zgłasza oferty
* 1.A.1. System po upływie czasu licytacji informuje [sprzedający](#ac1) o braku ofert za jego produkt.
* 1.A.2. Przejdź do kroku 13.
4.A. Podano niepoprawną kwotę
* 4.A.1. System informuje o błędnie podanej kwocie.
* 4.A.2. Przejdź do kroku 2.
11.A. Brak środków na saldzie
* 11.A.1. System informuje [kupujący](#ac2) o braku środków na saldzie.
* 11.A.2. System prosi [kupujący](#ac2) o wybranie innej formy płatności.
* 11.A.3. [kupujący](#ac2) wybiera inną formę płatności i dokonuje wpłaty.
* 11.A.4. Przejdź do kroku 12.

---

## Obiewkty biznesowe (inaczje obiekty dziedzinowe lub informatycjne)

### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupy produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę. 

### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.


<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujący](#ac2)ch, który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

## Macierz CRUDL


| Przypadek użycia                                  | Aukcja | Produkt |
| ------------------------------------------------- | ------ | ------- |
| UC1: Wystawienia produktu na aukcję               |    C   |    C    |
| UC2: Licytacja produktu                           |  R,U,D |  R,U,D  |


