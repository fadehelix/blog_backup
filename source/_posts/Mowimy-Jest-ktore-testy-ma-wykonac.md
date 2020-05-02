title: Mówimy Jest które testy ma wykonać
author: Adam Dziendziel
tags:
  - React
  - Testy
  - Jest
categories:
  - Tech
date: 2017-07-27 01:00:00
---
Ten post, to jedno z kilku planowanych przeze mnie praktycznych rozwinięć [tekstu o "Jest"](/testowanie-jest-wazne) - frameworku do testowania jednostkowego stworzonym przez Facebook , który to tekst pisałem mając jeszcze małe doświadczenie w testowaniu aplikacji "reactowej".   
Do rzeczy zatem.

## Komponent
Załóżmy, że mamy do przetestowania najprostszy komponent, którego zadanie to wyświetlić podany w "propsie" tekst i opakować go w nagłówek, jednak jeśli nie podamy tekstu, to nie chcemy aby jakikolwiek tag był generowany. Nazwijmy ten komponent... `Heading`.

{% codeblock Heading.jsx lang:javascript %}

/**
* Render H1 only if the value is not null nor empty string
*/
const Heading = ({value}) =>
  !!value && <h1 className="Heading"> {value} </h1>
    
export default Heading;
{% endcodeblock %}

## Podstawowy test
W zasadzie idąc za ideą TDD, lub jej bardziej kolorowym wariantem ["Czerwony, Zielony, Refactor"](http://itcraftsman.pl/red-green-refactor-testy-jednostkowe/) powinniśmy najpierw napisać testy, a dopiero potem implementację, ale kolejność dobrałem nieprzypadkowo. Otóż pierwszy test jaki mam zamiar napisać to test, wybaczcie mój klatchiański, [snapszotowy](https://facebook.github.io/jest/docs/snapshot-testing.html).

{% codeblock Heading.test.js lang:javascript %}
describe('Heading', () => {
  it('renders correctly', () => {
    const component = renderer.create(
      <Heading value="Nagłówek" />
    );
    expect( component.toJSON() ).toMatchSnapshot();
  });
});
{% endcodeblock %}

Powyższy test wygeneruje utworzy nam katalog `__snapshots__` a w nim plik o nazwie `Heading.test.js.snap` o następującej zawartości:

```
// Jest Snapshot v1, https://goo.gl/fbAQLP

exports[`Heading renders correctly 1`] = `
<h1
  className="Heading"
>
  Nagłówek
</h1>
`;
```

Jak widać komponent jest renderowany poprawnie.   
A dlaczego wolałem najpierw utworzyć komponent, a dopiero potem napisać "snapszota"? Ponieważ nie widzę sensu w pisaniu testów do nieistniejących jeszcze komponentów, a uświadomiłem to sobie przy pisaniu testów z właśnie tym typem asercji. Na ten moment bardziej przekonuje mnie kolejność Zielony -  Żółty - Czerwony, gdzie najpierw tworzę "minimal valuable component" (zielony), potem go refaktoryzuję (żółty), a w międzyczasie "watcher" może mi powiedzieć STÓJ! "wywalając" testy (czerwony).   
Mówiąc "watcher" mam na myśli domyślne zachowanie komendy `npm test` zaimplementowanej w [create-react-app](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#running-tests), gdzie aplikacja obserwuje zmiany na plikach i odpala testy za każdym razem automatycznie. Lubię to.

## Chcę odpalić tylko ten test
Zauważyłeś być może, że wbrew oficjalnej dokumentacji frameworka używam komendy `it()` zamiast `test()`. Ma to swoje uzasadnienie.

Otóż wspomniani antagoniści nie są tak naprawdę antagonistami, bo robią dokładnie to samo, ale różnica pojawia się, gdy chcemy powiedzieć Jest, które testy chcemy uruchomić, a których nie.

Załóżmy, że piszemy kolejny test, tym razem sprawdzający, czy komponent nie wyświetla się, gdy podamy mu pustą wartość:

```
it('doesn\'t render if its value is empty', () => {
    const component = renderer.create(
      <Subtitle value=""/>
    );
    expect( component.toJSON() ).toMatchSnapshot();
  })
```
Chcemy sobie zaoszczędzić czasu i nakazać silnikowi uruchamiać tylko aktualnie tworzony test. Możemy to osiągnąć zmieniając `it` na `fit` (od `f` jak focus):
```
fit('doesn\'t render if its value is empty', () => {
```
W efekcie wszystkie inne testy zostaną pominięte (skipped).

## Nie chcę aby ten test się uruchamiał
W bardzo podobny sposób możemy zapobiec wykonywaniu się danego testu.   
Wystarczy, że `it` zamienimy na `xit` (od `x` jak exclude):
```
xit('doesn\'t render if its value is empty', () => {
```

## Kontrola bloków
Powyższe dwie metody stosują się również do bloku `describe()`, odpowiednio `fdescribe()` oraz `xdescribe()`.

Więcej możesz się dowiedzieć z oficjalnej dokumentacji... Jasmine:   
* [fit](https://jasmine.github.io/2.1/focused_specs.html)
* [xit](https://jasmine.github.io/2.0/introduction.html#section-Pending_Specs)