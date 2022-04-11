title: Hello Debugger
author: Adam Dziendziel
tags:
  - ReactNative
  - DSP2017
categories:
  - Tech
date: 2017-05-05 17:40:00
---
Po tych kilku latach ciągłego uczenia się choćby w stopniu bardzo podstawowym nowych języków/frameworków/bibliotek doszedłem do wniosku, że pierwszą rzeczą jaką powinen się nowicujsz zainteresować nie jest wyświetlenie "hello world", tylko ogarnięcie sposobów na analizę działania pisanego kodu.    
Stąd zanim będę pisał o testach i implementacji, wrzucam krótką notatkę o podstawowych sposobach debugowania React Native.

## Narzędzia

### Debugowanie aplikacji w przeglądarce

Ale przecież tworzę aplikację mobilną, a nie stronę internetową!   
Nooo tak, ale to nic nie szkodzi.

Aby mieć taką mozliwość należy wejść do menu developerskiego w emulatorze (Dla androida jest to skrót `ctrl + m`) i wybrać __Debug JS Remotely__.   
Na wszelki wypadek można jeszcze "odświeżyć" aplikację naciskając dwa razy __R__.

 
[Instrukcja obsługi react-devtools](https://github.com/facebook/react-devtools/blob/master/packages/react-devtools/README.md)

### React Native Debugger

[React Native Debugger](https://github.com/jhen0409/react-native-debugger) to, najkrócej mówiąc, Chrome Dev Tools bez przeglądarki, działające jako samodzielna aplikacja.

![](/images/emulator-plus-rn-debugger.jpg)


Dwie wyróżniające cechy to:
1. [integracja debugera Redux](https://github.com/jhen0409/react-native-debugger/blob/master/docs/redux-devtools-integration.md). Póki co nie testowałem (tak szczerze to nawet nie użyłem jeszcze redux podczas swojej nauki), więc ciężko mi napisać jak bardzo to jest przydatne w praktyce.
2. Możliwość inspekcji drzewa DOM tak, jak stronę internetową. Niestety jest to bardzo ograniczone, jednak 

Debuger instalujemy [pobierając .zipa](https://github.com/jhen0409/react-native-debugger/releases) dla swojego systemu i, po rozpakowaniu, klikając plik wykonawczy _React Native Debugger_.

Możemy jeszcze doinstalować pakiet [react-native-debugger-open](https://github.com/jhen0409/react-native-debugger/tree/master/npm-package) zmieniający domyślny debuger z tego w Chrome na React Native Debuger właśnie. Niestety na Linux nie działa automatyczne otwieranie aplikacji w momenie uruchomienia emulatora. Kolejny świetny argument, by znienawidzić Apple jeszcze bardziej ;)


### Debugowanie w IDE
W poście o IDE dla React Native [wspomniałem](/IDEalny-edytor-dla-react-native), że postanowiłem się przyjrzeć Nuclide. Skusiła mnie m.in. możliwość debugowania aplikacji w IDE.    
Po bliższym przyjżeniu się tematowi, stwierdzam, że narazie odpuszczam, bo React Native Debugger spełnia swoją rolę. Być może wraz z doświadczeniem zaktualizuję tą sekcję, bo okaże się iż Nuclide daje jednak więcej, niż powyższe.

## Sposoby


### console.log() wiecznie żywy
Tak jak php ma swoją instrukcję `echo`, czy `print`, ruby ma `puts`, tak java script ma polecenie `console.log()`, które wyświetla zawartośc zmiennej, tablicy, czy obiektu w konsoli. W przypadku React Native konsolą jest konsola systemowa. Logi możemy przejrzeć poleceniem `$ react-native log-android` 

### Mój przyjaciel Breakpoint

Uzywanie tzw. _breakpointów_ to uniwersalny sposób na analizę działania kodu niezależnie w jakim języku jest napisany.  W skrócie metoda ta polega na oznaczaniu konkretnej linii kodu aby aplikacja zatrzymała swoje wykonywanie właśnie w tym miejscu.

W przypadku javascript możemy tego dokonać w przeglądarce bez konieczności konfigurowania swojego edytora.

W odróżnieniu do `console.log()` tutaj mamy w danym miejscu wyświetlony cały stan aplikacji z wszystkimi jej aktualnie wykorzystywanymi zmiennymi i obiektami.

Polecam obejrzeć [krótki screencast o używaniu break points w dev tools](https://egghead.io/lessons/react-using-the-chrome-debugger-to-set-breakpoints-in-react-native)  

## To nie koniec
Powyższy tekst jest tylko krótką notatką początkującego "reakt nejtiwa" i wraz ze wzrostem swojego doświadczenia będę go aktualizował, uzupełniał a także rozszerzał o kolejne pokrewne  posty. Także ten, stej tuned!
Póki co świetnym rozwinięciem jest lektura [oficjalnej dokumentacji](https://facebook.github.io/react-native/docs/debugging.html) React Native.

Polecam też zaparzyć sobie dobrą kawę i przeczytać [świetny artykuł o debugowaniu javascript](https://css-tricks.com/debugging-tips-tricks/) z którego ja też jeszcze dużo mogę się nauczyć :)