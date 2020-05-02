title: Lista w React Native
author: Adam Dziendziel
tags:
  - ReactNative
  - DSP2017
categories:
  - Tech
date: 2017-05-11 07:36:00
---
![Lista w React Native](/images/react-native-list-intro.jpg)

Przyszedł w końcu czas na stworzenie pierwszego widoku w mojej pierwszej aplikacji na React Native. Jest to lista zleceń jakie użytkownik aplikacji musi wykonać.

Bazuję tutaj oczywiście na aktualizowanej na bieżąco [specyfikacji funckjonalnej](https://relishapp.com/fadehelix/native-report/v/0-1/docs/specification/job-list).

## Definicja zlecenia

Póki co wiem, że zlecenie ma następujące parametry:
- Nazwa
- Opis
- Data
- Miasto
- Dokładna lokalizacja GPS

Pytanie jakie z tych informacji są mi potrzebne na liście? Na początek niech będą nazwa oraz miasto.
Wiem też, że na widoku listy chcę wyświetlać filtr zleceń.

## FlatList strzela focha
Po przejrzeniu komponentów do generowania listy elementów, wybrałem [FlatList](https://facebook.github.io/react-native/docs/flatlist.html), który postanowił dać mi do pieca i przy najprostszej implementacji robił cały ekran emulatora na czerwono sypiąc jakimiś ogólnymi komunikatami z core.   
Ten sam kod sprawdziłem na [Snacku](https://snack.expo.io) i tam wszystko pięknie zadziałało. Wniosek? Jak nie wiadomo o co chodzi (szczególnie w tak dynamicznie zmieniającym się środowisku jak RN) to z dużym prawdopodobieństwem chodzi o wersję.

### Upgrade React Native
Polecam przejrzeć [oficjalną dokumentację](https://facebook.github.io/react-native/docs/upgrading.html), tutaj tylko zanotuję jej streszczenie:

1. Najpierw należy zainstalować pakiet __react-native-git-upgrade__: `$ npm i -g react-native-git-upgrade`
2. Uruchomić zainstalowane narzędzie. Mi się nie udało bez podawania docelowej wersji react native, czyli musiałem wykonać komendę `$ react-native-git-upgrade 0.44.0`

Całe szczęście obeszło się bez konfliktów.

## React Native Elements i kolejny facepalm
Aby sobie uprościć i przyspieszyć kodowanie postanowiłem użyć bibliotekę komponentów z już zdefiniowanymi stylami. Tą biblioteką jest [react-native-components](https://react-native-training.github.io/react-native-elements/).

Bardzo fajna biblioteka, ale jest z nią trochę jak z Bootstrapem - niby pozwala szybko tworzyć interfejs, ale zgadzasz się na niepisaną zasadę, że bardzo nie chcesz tego dostosowywać do swoich precyzyjnych potrzeb. Dług technologiczny rośnie.

W moim przypadku są to dane wyświetlane w elemencie _ListItem_. Domyślnie ListItem ma dwa parametry "tekstowe": _Title_ oraz _Subtitle_. Czyli są __dwa__. Ja potrzebuję co najmniej __trzy__. Po przemyśleniu wybrałem następujące:
1. Nazwa zlecenia
2. Data
3. Miasto

Pierwsze podejście do rozwiązania tego problemu to nadpisanie w jakiś sposób komponentu ListItem. Jest to normalna klasa, więc może `extends`? Nie za bardzo, bo dziedziczenie ma swoje wady, a React jest stworzony do kompozycji dzięki [Higher Order Components](https://facebook.github.io/react/docs/higher-order-components.html). Znając ten wzorzec mamy większą motywację i zrozumienie aby tworzyć małe komponenty realizujące jedną funckjonalność. Wielbiciele TDD  właśnie uśmiechają się szeroko.

Cały dowcip (odkryłem go po jakimś czasie) polega na tym, że tutaj obejdzie się bez tworzenia kolejnego komponentu, bo... ListItem oferuje "wpakowanie" do parametru _subtitle_ całego [_View_](https://facebook.github.io/react-native/docs/view.html) (odpowiednika hatemelowego elementu _div_) a w nim dowolną ilość innych komponentów, w moim przypadku będą to dwa _Text_.

## Interakcja
Na koniec chcę, aby zlecenia (ListItem) reagowały na dotknięcie, więc dodaję właściwość __onPress__:
```javascript
...
onPress={() => this.onItemPress(item.id)}
...
```
Docelowo callback _onItemPress_ będzie przenosił użytkownika na ekran ze szczegółami wybranego zlecenia, ale to już historia na kolejnego posta.