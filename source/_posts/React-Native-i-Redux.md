title: React Native <3 Redux
author: Adam Dziendziel
tags:
  - DSP2017
  - ReactNative
  - NativeReport
  - Redux
categories:
  - Tech
date: 2017-05-17 23:00:00
---
![Tło grafiki znalezione na pexels.com](/images/react-loves-redux.png)

[W poście traktującym o implementacji listy zleceń](/React-Native-Nawigacja/) natrafiłem na problem przekazania do ekranu _JobDetails_ informacji o tym konkretnym zleceniu. Słowem, ekran nie miał pojęcia i nie obchodziło go, który element listy został wybrany, przez co nie mogłem na nim wyświetlić dynamicznej zawartości.   
Przekazać dane pomiędzy komponentami od _rodzica_ do _dziecka_ jest łatwo, wystarczy użyć "propsów, ale tutaj informacja o wybranym zleceniu musiała iść "w górę" czyli z `<JobItem />` przez `<JobList />` do głównego komponentu aplikacji, by zostać przekazana do innego ekranu. Użycie `react-navigation` też zwiększa złożoność, bo ta biblioteka ma zaimplementowaną własną logikę przekazywania danych pomiędzy komponentami.   
I tak sobie pomyślałem, że skoro i tak trochę czasu mi zajmie zbudowanie obsługi na eventach, to mogę równie dobrze nauczyć się czegoś pożytecznego, co przyda mi się wraz z rozwojem aplikacji.


## Brace your app, Redux is comming
Do tej pory, ucząc się Reacta, ignorowałem Redux jak się dało, aby sobie nie komplikować dodatkowo projektu, a także porządnie opanować zabawę propsami, stanami i eventami.

Dlaczego się jednak w końcu zdecydowałem na tak szalony krok?

Bo spodobała mi się idea zewnętrznego kontenera przechwytującego i magazynującego dane w czasie używania aplikacji.   
Słowo "czas" jest tutaj ważne, bo możemy łatwo poruszać się po historii akcji i generowanych przez nie stanów. Najlepiej to widać, gdy pobawimy się __Redux DevTools__ o którym wspominam na końcu tekstu - wybieramy akcję, klikamy przycisk _play_ i aplikacja odtwarza nasze inne akcje do teraźniejszości. 

Ja tutaj nie będę się rozpisywał o tym, czym jest Redux, bo sam mało go rozumiem, a doświadczenia mam tylda nic, natomiast czuję się na siłach polecić materiały z których czerpałem:

{% youtube 1w-oQ-i1XB8 %}

[Przykładowa integracja](https://github.com/react-community/react-navigation/tree/master/examples/ReduxExample) `react-navigation` z redux.   
I jeszcze [krótki opis  tegoż](https://reactnavigation.org/docs/guides/redux) .

A na deser świetna, [oficjalna dokumentacja Redux](http://redux.js.org/docs/basics/).

## Refactoring
Przede wszystkim musiałem zacząć od przeniesienia wsystkich ekranów do komponentu `<AppNavigator />`. To jest teraz moja baza, która "spina" całą aplikację i dopiero ona, ta baza, jest ładowana, po opakwaniu w reduxowy magazyn, do głównego komponentu aplikacji: `<NativeReport />`:

```javascript
<Provider store={this.store} >
	<AppWithNavigationState />
</Provider>
```
Ej! Chwila! Coś tutaj nie widać `<AppNavigator />`.   
No, fakt, a to dlatego, że po drodze ten komponent "dostaje" jeszcze stan nawigacji. Możesz to dokładnie zobaczyć w pliku [AppNavigator.js](https://github.com/fadehelix/NativeReport/blob/react-navigation-redux/src/navigators/AppNavigator.js)

Równie dobrze możnaby tego dokonać w `index.android.js`, ale jak już refaktorujemy, to usuwamy co się da z bazowego poziomu.

To, co jeszcze można zrobić, to "wyrzucenie"ekranów do osobnych plików i import ich w 'AppNavigator.js'

Po integracji z Redux, nowym sercem aplikacji jest [plik reducers/index.js](https://github.com/fadehelix/NativeReport/blob/react-navigation-redux/src/reducers/index.js) w którym definiuję jedyny narazie reducer oraz bazowy stan w tym przypadku będący przekierowaniem na listę zleceń.

Dla pełnego pdglądu zmian możesz zerknąć na [refaktoryzacyjnego brancha](https://github.com/fadehelix/NativeReport/tree/react-navigation-redux/src) w repozytorium projektu.

## JobDetails nareszcie ma co jeść
Krótkie sprawdzenie faktów:
1. Redux wszczepiony w ciało aplikacji - DONE
2. Pacjent żyje - DONE. 
3. Szczegóły są wyświetlane na ekranie zlecenia - DO...  znaczyyyy... eeeee, chwila!

Narazie aplikacja działa dokładnie tak, jak wcześniej.Dopiero teraz przyszedł czas na główny punnkt tego tekstu.

Spójrz na komponent [JobList](https://github.com/fadehelix/NativeReport/blob/react-navigation-redux/src/job-list.js):    
Przede wszystkim należy zmodyfikować propsa `onPress` przypisanego do `<ListItem />`:
```js
<ListItem onPress={ () =>
	dispatch(NavigationActions.navigate({ routeName: 'Job', params: item }))
} />
```
Kluczowy tam jest klucz `params` w którym do docelowego ekranu możemy przekazać np. obiekt. 

Stan z informacją o zleceniu mamy już ustawiony, wystarczy tylko te dane wyciągnąć w komponencie [JobDetails](https://github.com/fadehelix/NativeReport/blob/react-navigation-redux/src/job-details.js):

1. Wsadzamy mu, temu komponentowi, propsa zawierającego stan
```javascript
const mapStateToProps = state => ({
  nav: state.nav.routes,
});
```
2. Wyciągamy obiekt z danymi
```javascript
const JobDetails = ({nav}) => {
  if (!nav[nav.length - 1].params) {
    return <Text>There is no data for this job ;(</Text>
  }
  const jobDetails = nav[nav.length - 1].params;
  return (
    <Text style={styles.title}>{ jobDetails.name }</Text>
  );
};
```

## Debugowanie
[Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd/related) - rozszerzenie do Chrome, które daje nam możliwość czytelnej analizy stanów oraz "time traveling", czyli odtwarzanie stanu aplikacji w historii.
![Redux DevTools w działaniu](/images/rn-redux-devtools.jpg)
Domyślnie działa tylko z webowymi aplikacjami, ale...

.. możemy do naszej aplikacji React Native doinstalować [Remote Redux DevTools](https://github.com/zalmoxisus/remote-redux-devtools):
```
$ npm install --save-dev remote-redux-devtools
```
(trzeba jeszcze zmodyfikować nasz store poprzez dodanie drugiego parametru: `store = createStore(AppReducer, devToolsEnhancer());`)

## A po Redux przychodzą testy
Ale to już temat na osobny tekst. Póki co, mam tutaj jeszcze parę rzeczy do poprawy, bo np. nie wpadłem jeszcze jak dynamicznie ustawić tytuł ekranu no i oczywiście muszę sobie zaprojektować układ ekranu `JobDetails`.