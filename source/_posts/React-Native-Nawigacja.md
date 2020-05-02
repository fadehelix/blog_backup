title: 'React Native: Nawigacja'
author: Adam Dziendziel
tags:
  - ReactNative
  - DSP2017
categories:
  - Tech
date: 2017-05-12 13:52:00
---
![Grafika znaleziona na pexels.com](/images/blog-notes.jpeg)

Mam już przyzwoitą listę zleceń, teraz chciałbym, aby po dotknięciu konkretnego zlecenia przejść do jego szczegółów. Oficjalna dokumentacja zaprowadziła mnie do rozwijanej przez społeczność biblioteki [React Navigation](https://reactnavigation.org/docs/intro/).

Czas start.


## Ekrany
"Strony" pomiędzy którymi chcę się poruszać w apikacji mobilnej nazywają się __ekranami__ (_ang. screens_). React Navigation dostarcza nam mechanizm przełączania się, oraz prostą animację przejścia.

Pierwsza rzzecz, którą robię, to refaktoryzuję klasę _ReactNative_ w pliku [index.android.js](https://github.com/fadehelix/NativeReport/blob/master/index.android.js). Do tej pory był to główny komponent aplikacji do którego dodawałem własne komponenty.   
Zmieniłem jego nazwę na _HomeScreen_ dodają  wymagane przez _Navigation_ `static navigationOptions = { ... }`.

Storzyłem też kolejny ekran zawierający komponent _JobDetails_. Nazwałem go _JobScreen_.

Teraz głównym komponentem aplikacji jest lista ekranów:

```javascript
/**
 * Screens
 */
const NativeReport = StackNavigator({
  Home: { screen: HomeScreen },
  Job: { screen: JobScreen }
});
```

Narazie nie "wyrzucam" komponentów ekranów do osobnych plików. Na to przyjdzie czas, gdy aplikacja się rozrośnie.

## onPress

Mamy ekrany, ale nie możemy jeszcze się pomiędzy nimi poruszać. To jest czas na dodanie interakcji.

Refaktoruję _JobList_, aby zdarzenie _onPress_ komponentu _ListItem_ przyjmowało właściwość _onPress_ rodzica.

```javascript
<ListItem onPress={() => this.props.onPress()}/>
```

Dzięki  temu mogę do _JobList_ przekazać funkcję _navigate()_

```jsx
<JobList onPress={() => navigate('Job')} />
```

W tym momencie mogę "pacnąć" element listy i zobaczę  ekran _JobList_. Z automatu dostajemy też "cofnięcie" się do listy. Nie musimy sami tego kodować. 

## I'll be back coder fucker
Tutaj miał być opis jak przekazać do _JobDetails_ informację o tym, które zlecenie nacisnął użytkownik. Temat jest troszkę bardziej złożony, bo będzie wymagał zabawy z propagacją zdarzeń. Słowem, dobry temat na osobny wpis. 

Stay tunned!