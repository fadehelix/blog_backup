title: Testowanie JEST ważne
author: Adam Dziendziel
tags:
  - ReactNative
  - React
  - Testy
  - Jest
  - Enzyme
categories:
  - Tech
date: 2017-05-31 18:00:00
---
![](/images/post-jest-1-intro.jpeg)

W końcu zawziąłem się, włączyłem kamerę w laptopie i powiedziałem sobie stanowczo w twarz, że czas najwyższy na pisanie testów. Twarz, którą widziałem na monitorze nie była specjalnie szczęśliwa po usłyszeniu tych słów, bo przecież zwolni tempo rozwijania samej aplikacji. Liczą się przecież implementowane ficzery.

Spojrzenie na sprawę trochę zmieniło się, gdy powyższe twierdzenie zmodyfikowałem do postaci __liczą się implementowane ficzery co do których mam pewność że działają__.

## Nie cierpię stresu!
To publiczne wyznanie to trochę strzał w kolano, bo programiści umiejący pracować pod dużą presją są bardzo cenieni. Ja presję czasu lubię, wręcz jej potrzebuję do wydajnej pracy, pod warunkiem jednak, że _jest_ to presja zdrowa,  umiarkowana.   
Maciej Aniserowicz nagrał ostatnio dobry [podcast o stresie](http://devstyle.pl/2017/05/22/devtalk56-o-stresie-i-porazkach-z-krzysztofem-skubisem/).

Stres jakiego nienawidzę w tej pracy związany _jest_ głównie z obawą, że po deployu coś gdzieś w aplikacji się posypie. To przykre uczucie potęguje się w średnich i dużych projektach, gdzie z jednej strony każdy niedziałający element to konkretne straty dla klienta, a z drugiej proces wdrażania poprawek na produkcję _jest_ złożony, czytaj: trwa relatywnie długo, bo _jest_ zależny od CI, albo - co gorsza - od jakiś manualnych czynności innych osób. Pozdrawiam "Mordor" i biednych orków. 

I to _jest_ właśnie mój podstawowy powód do dokładania czasu na pisanie testów. Oczywiście jakość też _jest_ ważna, ale mój święty spokój _jest_ ważniejszy i basta!

Pytanie, czy w ekosystemie React (Native) _jest_ jakieś dobre narzędzie do testowania aplikacji? 

## Jest!
`Warning! Suchar intesifies!`

Eh...

[Jest](https://facebook.github.io/jest/) to, rozwijany przez pracowników Facebooka plus społeczność, framework, którego jednym z podstawowych założeń _jest_ prostota użycia i szybkość testowania. Wiele ficzerów, takich jak asercje, czy "test runner" mamy gotowe do użycia od razu.  
Dla mnie jego podstawową zaletą na ten moment _jest_ bardzo łatwa integracja z React Native.


Jest został stworzony z myślą o testach jednostkowych. Teoretycznie możemy pisać klasyczne asercje, które w Jest są nazywane ["matchers"](https://facebook.github.io/jest/docs/en/using-matchers.html#content).    
Oto przykład bardzo precyzyjnego testowania wyniku dodawania:
```js
test('dwa plus dwa', () => {
  const value = 2 + 2;
  expect(value).toBeGreaterThan(3);
  expect(value).toBeGreaterThanOrEqual(3.5);
  expect(value).toBeLessThan(5);
  expect(value).toBeLessThanOrEqual(4.5);
  expect(value).toEqual(4);
});
```
Jednak _jest_ coś, co spowodowało zmarszczenie się mojego smagłego lica z powodu bolesnego niezrozumienia tego co czytam, a potem radosnego uśmiechu dziecka odkrywającego, że lodówka _jest_ pełna czekolady.

### Hello snapshots
Tymi łakociami są Snapszoty (duża tabliczka Milki z żelkami dla tego, kto zagureuje mi sensowne tłumaczenie tego terminu na polski). Na początku nie mogłem zrozumieć idei, bo _jest_... inna, niż testowanie do którego się przyzwyczaiłem.     
* Nie ma asercji.    
* Po pierwszym uruchomieniu pojawia się kalog \__snapshots\__ a w nim jakiś dziwny plik z rozszerzeniem _.snap_  

O co chodzi?

Idea przewodnia jest taka, że wszyscy chcą mieć pewność, że wszystkie komponenty wciąż dobrze się renderują. Jest przy każdym przebiegu porównuje snapshoty (będące w praktyce plikami JSON) i, jeśli sie różnią, wyświetla stosowną informację z zapytaniem czy chcemy zatwierdzić nasz różniący się od poprzedniego wynik testu (bo zmiany, które nastąpiły były celowe).


## A co z Enzyme?
Jeśli zależy nam na bardziej klasycznym testowaniu komponentów, to warto zainteresować się biblioteką [Enzyme](http://airbnb.io/enzyme/).     
_Jest_ ona polecana nawet w [oficjalnej dokumentacji](https://facebook.github.io/react/docs/test-utils.html#overview) Jest.
Z kronikarskiego obowiązku notuję tylko na marginesie, że polecanym na [stronie dokumetacji](https://facebook.github.io/react/docs/test-utils.html#overview)  narzędziem _jest_ .   

Ważna informacja: Jest i Enzyme to __nie są konkurencyjne rowiązania__, ponieważ ten pierwszy to framework w ramach którego __można__ używać ten drugi.

Na pewno jeszcze wrócę do tego tematu i zaktualizuję ten ten tekst.


## Coby nie zapomnieć

[Husky](https://github.com/typicode/husky) to instalowany przez npm jako _dev dependency_ w projektcie zestaw [gitowych hooków](https://git-scm.com/book/gr/v2/Customizing-Git-Git-Hooks) (_haków?_ brrr...) do których możemy przypisać dowolne akcje takie jak uruchamianie testów przez commitem.   
Wystarczy dodać do sekcji `scripts` w naszym _package.json_:
```js
{
  "scripts": {
    "precommit": "npm test",
    "prepush": "npm test",
    "...": "..."
  }
}
```
Husky świetnie sprawdza się w małych projektach, gdzie testy nie zajmują dużo czasu, a i często nie uważamy za konieczne konfigurowania i podpinania żadnego  [CI](http://www.code-maze.com/what-is-continuous-integration/) takiego jak darmowe dla projektów opensource [Travis](https://travis-ci.org/) i [AppVeyor](https://www.appveyor.com) (dla aplikacji mających działać pod Windows). 

Jedna uwaga: Jeśli korzystamy z `create-react-app` i "watchera" testującego aplikację przy każdej modyfikacji (uruchamianego komendą `$ npm test`) to wtedy nie dość, że nie potrzebujemy Husky, to go też nie chcemy, bo jeśli commit uruchomi test, to włączy się "watcher" i z commitu nici. Smutek. 


## Linkografia
Na koniec lista zasobów, które pomogły mi lepiej zrozumieć zagadnienia związane z testowaniem React:
* [Testing React application with Jest](https://auth0.com/blog/testing-react-applications-with-jest/)
* [Unit Testing React components with Jest](https://www.vinta.com.br/blog/2017/unit-testing-react-components-jest/)
* [Unit Testing React Components: Jest or Enzyme?](https://www.codementor.io/vijayst/unit-testing-react-components-jest-or-enzyme-du1087lh8)