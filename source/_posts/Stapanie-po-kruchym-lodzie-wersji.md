---
title: Stąpanie po kruchym lodzie wersji
tags:
  - DSP2017
  - ReactNative
  - npm
author: Adam Dziendziel
categories:
  - Tech
date: 2017-05-13 18:21:00
---


![](/images/npm-wersje-rn-intro.jpg)

Muszę się do czegoś przyznać. Dzisiaj, najprawdopodobniej pod wpływem optymizmu wywołanego słońcem i wiosennym ciepłem, odpaliłem komendę `npm update` w projekcie.   
Projekt podziękował mi moim ulubionym, czerwonym ekranem emulatora.   
Miłość między developerem a jego dziełem bywa trudna.

## Zamrażanie wersji
Jeśli już o lodzie wspomniałem, to kluczowym tematem jest precyzyjna kontrola wersji bibliotek jakich używamy. Szczególnie w tak dynamicznie ewoluującym ekosystemie jak RN. Szczególnie, gdy mamy w zależnościach wersję beta jakiegoś pakietu. Szczególnych przypadków, które nie lubią abyśmy byli produktywni, jest dużo.



## ~ vs. ^
Ten enigmatyczny nagłówek jes ważny w kontekście aktualizacji.
W skrócie:

__~__ oznacza, że aktualizacja podniesie nam tylko ostatnią cyfrę do najwyższej możliwej, czyli z wersji 1.0.1 zrobi nam się 1.0.4

__^__ jest bardziej "luźne" i może nam podnieść także drugą cyfrę: z 1.0.1 na 1.2.1

Nauczyłem się tego ze [Stackoverflow](http://stackoverflow.com/questions/22343224/whats-the-difference-between-tilde-and-caret-in-package-json) :)

Ale o co chodzi z tymi liczbami i dlaczego to takie ważne? Pakiety node stosują tzw. _Semantic Versioning_, w skrócie [semver](https://www.sitepoint.com/semantic-versioning-why-you-should-using/).
Najprościej mówiąc polega to na tym, że:
- __trzecia cyfra__ w numerze wersji ( np. 1.0.__1__) oznacza numer pacza (łatki ?) i nic nie zmienia w zachowaniu biblioteki.
- __druga cyfra__ w numerze wersji (np. 1.__2__.1) oznacza zmiany kompatybilne wstecznie, czyli możemy założyć iż nie istnieje ryzyko wysypania się aplikacji przy podnoszeniu wersji.
- __pierwsza cyfra__ w numerze wersji (np. __1__.3.0) może oznaczać wszystko, łącznie z armagedonem i deszczem ryb w projekcie.

## Rosyjska ruletka z npm install
To jest główny punkt, niejako podsumowujący dwa powyższe. Otóż pójście na łatwiznę i po prostu uruchomienie komendy `npm install nazwa-zajebistej-biblioteki` powoduje, że mamy słabą kontrolę nad tym co instalujemy i prosimy się przez to o problemy. Trochę tak jak ze ślizganiem się po tafli jeziora pomiędzy przeręblami - w którymś miejscu możemy nie wyhamować i wpaść do wody. Bardzo zimnej wody. Na bardzo odludnym jeziorze.

Najlepszym podejściem jest ręczne dodanie biblioteki do _package.json_ i przyjrzenie bibliotekom od niej zależnym. Czyli też warto z góry znać przynajmniej podstawowe biblioteki jakie będziemy używać.

Nauczyłem się tego na przykładzie _react-native-elements_ które wymagają zainstalowanej _react-native-vector-icons_. Tak to wygląda w moim package.json:
```json
"dependencies": {  
...
	"react-native-vector-icons": ~4.0.0,                                                                                                                             
	"react-native-elements": "^0.11.2"
...
}
```
To działa.   
Co było nie tak?    
`npm install react-native-vector-icons` dodał do konfiguracji coś takiego: `"react-native-vector-icons": ^4.1.1`. Czyli najnowszą stabilną wersję. 

Tutaj się właśnie nauczyłem o "bezpiecznikach" w postaci znaków rozpocynających numer wersji. Zmiana __^__ na __~__ powoduje, że mogę bezpiecznie robić update aż do momentu w którym _react-native-elements_ będą mieć w zależnościach ikony z jedynką na drugiej pozycji. 

W ramach darmowego bonusu nauczyłem się też, że druga cyfra potrafi jednak namieszać, cwana bestia, choć nie bezpośrednio.


## Clear Cache na ratunek (prawie) zawsze
W razie, gdy nie mamy pojęcia co się dzieje warto "przeinstalować" zależności w naszym projekcie. Oto podstawowa lista instrukcji, którą można sobie zamknąć w jednym skrypcie w stylu `fakju-react.sh` ;)
```bash
watchman watch-del-all
rm -rf node_modules
npm cache clean
npm install
npm start --reset-cache
```
Przy czym pierwsza linia zakłada, że w systemie mamy zainstalowany [watchman]() który nie jest obowiązkowym narzędziem do rozwijania aplikacji RN, ale przydatnym choćby ze względu na zwiększenie szybkości kompilacji.

## Higiena wersji
Tak sobie pomyślałem, w ramach podsumowania, że warto podczas każdej iteracji poświęcić trochę czasu specjalnie na zarządzanie wersjami i zależnościami aby być na bierząco z aktualizacjami i uniknąć dużego stresu, gdy kiedyś jednak będziemy musieli zaktualizować projekt, bo, na ten przykład, nie dodamy nowej wypasionej biblioteki, która załatwia nam wszystkie problemy, oprócz tego, że wywala nam całą aplikację, bo zaniedbaliśmy jej systematyczne aktualizowanie i testowanie.

Dzięki za dotrwanie do końca artykułu.   
Jeśli Ty masz jakieś doświadczenia w temacie to chętnie przyjmę w komentarzach wszelkie sugestie i porady.     
Yo!