title: Projektowanie komponentów podczas pisania testów
author: Adam Dziendziel
tags:
  - React
  - Jest
  - TDD
categories:
  - Tech
date: 2017-10-25 19:00:00
---
![](/images/unit-tests-spec-intro.jpeg)

Niniejszy tekst to krótkie rozwinięcie [posta o traktowaniu testów jako dokumentacji funkcjonalnej](/Testy-jednostkowe-jako-dokumentacja) na poziomie komponentu lub modułu.


## Projektowanie komponentu podczas pisania testów
Dzięki temu, że do testów musimy użyć komponent w taki sam sposób w jaki go użyjemy w aplikacji, to praktycznie widzimy jakie właściwości (ang. props) potrzebujemy. Można to nazwać podejściem _api-first_ ponieważ najpierw "projektujemy" zewnętrzne parametry komponentu, a dopiero potem je implementujemy.
Ja się o tym przekonałem tworząc komponent mający za zadanie wyświetlić "zajawkę" artykułu na blogu.

__Źle__    
Najpierw, __przed napisaniem testów__, stworzyłem sobie komponent `PostSummary`, który przyjmował tylko jedną właściwość "post", która była obiektem zawierającym dane posta, czyli jego id, tytuł, zawartość, datę utworzenia itd.   
Z punktu widzenia implementacji było to bardzo wygodne i elastyczne podejście, bo w przyszłości mogłem sobie dowolnie modyfikować dane wyświetlane przez komponent nie przejmując się tym, co jest na wejściu.

```html
<PostSummary post={{id: 1, title: "Pierwszy artykuł", summary: "Treść zajawki artykułu"}} />
```

W pliku `PostSummary.test.js` najpierw utworzylem _stuba_, czyli "sztuczny" obiekt odzwierciedlający dane przyjęte z CMS:
```js
const post = {
  "id": 2,
  "slug": 'display-me',
  "status": true,
  "title": "Display me",
  "created": 1503246542,
  "summary": "Dolore jugis nutus. Abluo imputo incassum obruo proprius roto saepius utrum voco volutpat. Blandit damnum eligo ibidem. Abbas tum ut. Adipiscing euismod gravis ideo probo proprius. Aptent euismod luctus nunc wisi ymo. Autem decet macto melior neque proprius refero valde. Antehabeo consectetuer eligo paratus patria ratis tum vindico vulputate."
};
```
Następnie napisałem test pokazujący co się renderuje za pomocą snapszota:
```js
it('renders correctly', () => {
    const component = renderer.create(
    <PostSummary post={post}/>
  );
  expect(component.toJSON()).toMatchSnapshot();
});
```

Dlaczego to nie jest dobre podejście?   
Ponieważ komponent z czarnej skrzynki zwracającej przetworzone dane wejściowe staje się puszką Pandory po której nie wiadomo czego się spodziewać. Teoretycznie, gdy używamy snapszotów, to nam to nie przeszkadza, bo testy pokazują nam różnice w zawartości generowanej przez komponent.    
Ale nie tłumaczą dlaczego nastąpiły zmiany, bo w obiekcie `post` może być wszystko, albo też może brakować jakiegoś parametru.

No więc mam sobie komponent, czas napisać testy sprawdzające, czy działa.

__Dobrze__    
W tym momencie zacząłem się zastanawiać jak przetestować przypadek, gdzie `post.status` ma wartość "false". Oczywiście tworzę nowy obiekt `post` z innymi wartościami parametrów i niby wszystko gra. Pomyślałem sobie jednak, że to mało czytelne, że to słaba dokumentacja jest.   
No więc napisałem sobie nowy przypadek testowy z inaczej zdefiniowanymi parametrami komponentu:
```js
it('renders correctly', () => {
  const component = renderer.create(
  <PostSummary title={post.title} summary={post.summary} id={1} display={false}/>
  );
  expect(component.toJSON()).toMatchSnapshot();
});
```
Teraz użycie <PostSummary /> jest o wiele bardziej przejrzyste, a gdy dodamy do niego [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html) to już w ogóle będziemy mieć bardzo dużą kontrolę nad tym, co w ogóle "wpada" do komponentu.   
Dodatkowy bonus jest taki, że zdefiniowanie właściwości komponentu zanim zaczniemy go kodować może spowodować znacznie bardziej przemyślaną i czytelniejszą implementację.

## A może by tak dodać obsługę błędów?
Nieoczekiwanym efektem ubocznym podania całkowicie innych właściwości komponentu (oczekiwał `data` a dostał `title`, `summary`...) był komunikat

```bash
The above error occurred in the <PostSummary> component:
    in PostSummary (at PostSummary.test.js:32)
    in Router (created by MemoryRouter)
    in MemoryRouter (at PostSummary.test.js:31)
    
Consider adding an error boundary to your tree to customize error handling behavior.
You can learn more about error boundaries at https://fb.me/react-error-boundaries.
```
Konsola podsunęła mi całkiem dobry pomysł, aby dodać wprowadzoną w React 16 [obsługę błędów](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html). I to jest temat, który rozwinę w kolejnym poście.

## Prośba na koniec
Będę wdzięczny za feedback, czy powyższy tekst jest jakościowo wart zużycia na jego przeczytanie Twojego cennego czasu. Zdaję sobię sprawę, że w tak jednostronnej komunikacji jaką jest tekst na blogu mam problemy z precyzyjnym wyrażaniem swoich myśli oraz że wiele rzeczy podświadomie zakładam.   
Dla mnie ten tekst jest użyteczną notatką, bo znam doskonale kontekst jej powstania, ale chcę wiedzieć, czy ktoś szukający konkretnych informacji jest je w stanie znaleźć.
Z góry dzięki!

