title: 'Snack, czyli Codepen dla React Native'
author: Adam Dziendziel
tags:
  - DSP2017
  - ReactNative
  - Tools
categories:
  - Tech
date: 2017-04-27 01:29:00
---
![Screen Snacka](/images/snack-codepen-intro.jpg)

Wpadam tutaj na bloga tylko na chwilę, aby zanotować parę słów o  moim najnowszym znalezisku, ciekawym narzędziu ułatwiającym praktyczną naukę React Native oraz eksperymenty i dzielenie się kodem.    

## Drodzy Państwo, oto  [Snack](https://snack.expo.io/)!
Niech pierwszy naciśnie _delete_, kto nigdy nie słyszał o [Codepen.io](http://codepen.io/) . Świetne narzędzie do nauki, zespołowego prototypowania animacji, elementów interfejsu webowego , czy wreszcie [źródło inspiracji](http://codepen.io/pens/).

No więc, robiąc codzienny przegląd Twittera, trafiłem na [prezentację o React Native](https://vimeo.com/214606707), gdzie niejaki [Tom Wilson](https://twitter.com/twilson63) zaczął od podstaw po czym wyciągnął armatę większego kalibru i wystrzelił mi prosto w mózg pokazując demo Snacka.   

{% twitter https://twitter.com/CHSdigital/status/856849492825526277 %}

No i faktycznie to działa jak Codepen, tylko że nie ma tu wyboru bibliotek. Jest tylko RN. Automatycznie tworzy się adres, który możemy podesłać komuś aby się pochwalić swoim super komponentem, jest też __możliwość embedowania__ (wybacz ten ponglisz, ale "osadzanie" nie przechodzi mi przez palce) kodu na swojej stronie.   
Tylko uwaga, bo każdy zapis (przycisk _"Save changes"_) __zmienia nam URL__. Ma to swoje zalety i wady, ale warto mieć to na uwadze, szczególnie, jeśi nie jesteśmy zalogowani.

Świetną sprawą są też ciekawe __predefiniowane komponenty__ (takie cuda jak Facebook Login, Google Login, MapView, czy akcelerometr), które możemy dodać poprzez przzeciągnięcie je do edytora, a tam już pojawi się niezbędny kod. Emotka pulsującego serduszka.

Jeszcze mała, ale istotna sprawa: czytałeś mój [post o wyborze edytora](/IDEalny-edytor-dla-React-Native) lubiącego się z RN? Jeśli nie, to nic nie straciłeś, bo stwierdzam, niesiony falą entuzjazmu, że __Snack i tak jest lepszy__. 

## Bohater drugoplanowy: Expo
Snack to nie tylko świetny edytor kodu.
Pisany kod mogę bardzo szybko uruchomić na __własnym telefonie__.
Wystarczy, że zainstaluję [aplikację Expo](https://play.google.com/store/apps/details?id=host.exp.exponent) a następnie za jej pomocą zeskanuję kod QR ze Snacka. 

![Screen z mojego telefonu](/images/snack-screenshot-phone.png)

W tym momencie, dzięki [Hot Reloading](https://facebook.github.io/react-native/blog/2016/03/24/introducing-hot-reloading.html),  mam na żywo podgląd zmian w pisanej apce.  Jest to super, bo nie trzeba za każdym razem budować aplikacji od nowa po zapisaniu zmian w kodzie.

Tak naprawdę Expo to cała platforma do tworzenia aplikacji z wykorzystaniem React Native i na pewno jeszcze bliżej się jej przyjrzę. I oczywiście opiszę swoje eksperymenty na tym blogu.      
Póki co, uważam, że dodanie Expo do projektu niepotrzebnie zwiększy jego złożoność pomny zasady, że każda nowa biblioteka dodana do projektu zwiększa nasz dług technologiczny.

## Android? iOS? Proszę bardzo!
Oprócz testowania pisanej aplikacji na swoim telefonie można użyć emulatora w przeglądarce.      
O ile nie robi to na mnie wrażenia jeśli chodzi o Androida (bo Android Studio i jego AVD), o tyle kodując na Ubuntu fajnie mieć możliwość podejrzenia aplikacji uruchomionej na iOS. I działa to szybko.

## Kurtyna opadła, światła gasną
To przedstawienie będzie miało ciąg dalszy, gdy już opanuję podstawy developmentu aplikacji. Na razie uważam, że to może być dobre narzędzie na rozwinięcie mojej aplikacji, lub lekarstwo na jakiś gruby bloker.

Jeszcze tylko na odchodnym wręczę Ci kilka linków:    
[Bardzo dobry artykuł o Snack i Expo](https://blog.expo.io/sketch-a-playground-for-react-native-16b2401f44a2)    
[Mój pierwszy snack](https://snack.expo.io/r1s9gO0Ae)   
Jeszcze raz [prezentacja o RN](https://vimeo.com/214606707). Tak, uważam, że jest aż tak dobra, że muszę powielić link do niej w tym artykule.