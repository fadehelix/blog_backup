title: Testy jednostkowe jako dokumentacja
author: Adam Dziendziel
tags:
  - Jest
  - Testy
  - TDD
  - React
categories:
  - Tech
date: 2017-10-20 01:00:00
---
![](/images/unit-tests-spec-intro.jpeg)

Po tekście o tym dlaczego [testowanie jest ważne](/testowanie-jest-wazne/) dla mojego zdrowia psychicznego, przyszła pora na zanotowanie kolejnego aspektu motywującego pisanie testów jednostkowych. 

## Hasztag TDD
Napewno słyszałeś określenie Test Driven Development (TDD), czyli podejście do rozwijania oprogramowania, które zakłada pisanie testów __zanim__ zaczniemy w ogóle pisać implementację (właściwy kod). Słyszałeś że to jest dobre? Słyszałeś, że to jest zuo? Ja mam wrażenie, że ilu jest programistów tyle jest opinii i wariacji TDD. Ja sam nie jestem przekonany, być może dlatego że obracam się w świecie małych projektów z ograniczonym czasem.

Pisanie masy kodu zanim w ogóle zabiorę się za rozwiązywanie właściwego problemu jest bardzo drogie, a ja jestem bardzo biedny.


## A co jeśli testy nazwiemy specyfikacją?
O [Living Documentation](/Projektowanie-behawioralne/) już kiedyś napisałem w kontekście BDD, ale całkiem niedawno, po obejrzeniu [serii tutoriali o Redux](https://egghead.io/courses/getting-started-with-redux), dotarło do mnie w końcu, że zamiast koncentrować się na wymyślaniu granicznych przypadków wystarczy że zastanowie się dokładnie co tak naprawdę mój komponent, lub funckja ma dokładnie robić (oraz czego nie powinien).    
A że w dodatku jestem kinestetykiem i myślę działając, to czas poświęcony na opisanie działania funkcji za pomocą testów spłaca mi się potem podczas implementacji w postaci o wiele bardziej przemyślanego kodu.  
A przypadki graniczne? Na ich napisanie przyjdzie czas podczas najbliższej refaktoryzacji.

## Przykładowa specyfikacja
Weźmy na tapetę prostą funckję zamieniającą tytuł artykułu na poprawny [slug](), czyli adres url tegoż tekstu.

### Krok 1: Test, czyli definiuję co funckja ma robić (test)
```javascript
describe('Slug', () => {
  it('replace all spaces with dashes and trim', () => {
    expect(Url.getSlug( 'this is a post title' )).toBe('this-is-a-post-title');
  });
  it('trims given string', () => {
    expect(Url.getSlug( ' this is a post title ' )).toBe('this-is-a-post-title');
  });
  it('replace dotes with dashes', () => {
    expect(Url.getSlug('this.is.dot')).toBe('this-is-dot');
  });
  it('remove commas', () => {
    expect(Url.getSlug('this,is,comma,')).toBe('thisiscomma');
  });
});
```
Oto efekt uruchomionego testu, gdzie elegancko widać czego oczekujemy od fukcji, którą musimy zaimplementować.
![](/images/first-run-red.png)

## Krok 2: Implementacja, czyli piszę właściwą funkcję
Dzięki użyciu [lodash](https://lodash.com/) implemenctacja okazała się nadspodziewanie prosta:
```
const getSlug  = path  => {
  return _.kebabCase(path);
};
```
Z racji tego, że metoda `kebabCase()` domyślnie zamienia przecinki na myślniki, zdecydowałem zmienić asercję, która wcześniej zakładała po prostu usunięcie tych znaków przystankowych. Nie miałem sztywnych wymagań, więc mogłem.

Teraz wszystkie testy przeszły:
![](/images/all-green.png)

W tym momencie mam zdefiniowane najważniejsze zachowania funkcji, oraz właściwy kod i mogę brać się za następne zadanie, bo czas goni.

A jeśli jakimś niezwykłym zbiegiem okoliczności mam jeszcze trochę czasu na aktualne zadanie? 

## Krok 3: Bonus, czyli co by było gdyby...
Tutaj można dać upust kreatywności jak zepsuć funkcję i testować różne przypadki brzegowe i obserwować wyniki testów. Fajne jest to, że zostanie to w postaci napisanego scenariusza, a nie "sprawy dla testera".

Ja na ten przykład postanowiłem sprawdzić co się stanie, gdy w tytule posta znajdą się dowolne znaki interpunkcyjne:
```
  it('Remove questions, quotations etc', () => {
    expect(Url.getSlug('to jest! tekst? z "cytatem"')).toBe('to-jest-tekst-z-cytatem')
  });
  ```
Okazało się, że twórcy lodash o tym pomyśleli i wykrzykniki, pytajniki itp. są po prostu usuwane.

#### toBe czy isEqual?
To taka mała dygresja dotycząca dwóch asercji w Jest, które teoretycznie robią to samo, ale jednak nie do końca, gdyż jak się okazuje:
- __toBe()__ jest odpowiednikiem `===`i działa "płytko", to znaczy, że jeśli oczekujemy obiektu to on sprawdzi, czy na wyjściu jest obiekt, ale nie sprawdzi jego właściwości i metod. W moim przypadku to zupełnie wystarcza, bo porównuję ciągi znaków.
- __isEqual()__ działa trochę wolniej, ale "dokładniej", czyli sprawdzi nam zawartość obiektu, czy tablicy. 

## TDD? Tak, ale nie
Przykład, który podałem jest, pomimo iż wyjęty z mojego prawdziwego projektu, bardzo trywialny, ale opisane powyżej podejście wypracowałem sobie w testach, gdzie następują symulacje kliknięć, czy pobieranie danych ze (zmockowanego) zewnętrznego API. Taka specyfikacja świetnie uzupełnia się ze [snapszotami Jest](https://daveceddia.com/snapshot-testing-react-with-jest/), chociaż one akurat mają sens dopiero po implementacji komponentu.

Według mnie pisanie bardziej specyfikacji, niż testów i myślenie o nich w ten sposób, pozwala na zaoszczędzenie sobie czasu na pisaniu scenariuszy (bo zastanawiamy się tylko nad najważniejszymi przypadkami) oraz zminimalizowaniu problemów z kodem w przyszłości, bo jednak testy są.

Jeśli spojrzymy na naszą specyfikację jeszcze szerzej i potraktujemy ją jako "living documentation" to mamy fajnie opisane funkcjonalności dokumentacją, która na sto procent jest zawsze aktualna (bo gdyby nie była to testy by nie przechodziły i nasz build by się "wywalał").