title: IDEalny edytor dla React Native
author: Adam Dziendziel
tags:
  - DSP2017
  - ReactNative
  - Tools
categories:
  - Tech
date: 2017-04-25 20:05:00
---
![](/images/react-native-choose-ide.jpg)

Na wtępie muszę zaznaczyć, że od kilku lat jestem fanboyem IDE od JetBrains. O użyciu RubyMine już pisałem w poście o pisaniu ficzerów Cucumber, Android Studio także odeszło od Eclipse na rzecz InteliJ, do php tylko PhpStorm, a ostatnio, ucząc się react testuję jego lżejszego brata - Webstorm. I jestem bardzo zadowolony.

Niemniej z czystej ciekawości zapytałem mojego wyśmienitego mentora i oddanego przyjaciela Gogle: "react native best ide"

Szybki przegląd pierwszych kilku wyników i głównym kandydatem na alternatywę został...

## Atom

... a właściwie [Nuclide](https://nuclide.io/), będący tak naprawdę pluginem Atoma, który już kiedyś testowałem, więc mam zainstalowany. No super.
I pierwszy zonk - Nuclide wymaga Atom w wersji >= 1.16, więc dmuchnąłem mocniej i spod kurzu moim oczom ukazala się wersja... 1.6   
No więc update, ale to nie takie proste, bo Atom na Ubuntu nie ma opcji aktualizacji samego siebie, więc szybkie zerknięcie na readme w repozytorium Atom, a tam krótki dowcip o tym, że aby zaktualizować trzeba za każdym razem pobrać paczkę atom-amd64.deb i zainstalowac manualnie.     
Za każdym razem, gdy chcemy zaktualizować edytor. Aż z sentymentu do starych czasów się wzruszyłem.

![](/images/instalacja-atom-ubuntu.jpg)


Po uruchomieniu Atom, przejściu do Ustawień i zakładki "Install" Nuclide łaskawie pozwolił mi się zainstalować. Udawaj, że widzisz w tym miejscu emotkę serduszka. 

![](/images/instalacja-nuclide.jpg)

Tak na marginesie, skoro już przy pluginach jesteśmy - polecam gorąco '[keybinding-cheatsheet](https://atom.io/packages/keybinding-cheatsheet)', który wyswietla w panelu po prawej wyszukiwarkę skrótów klawiszowych. Dowiedziałem się dzięki temu, że do ustawień edytora można się dostać skrótem _Ctrl + ,_

Tutaj jest fajna instrukcja [instalacji Nuclide na Ubuntu](https://nuclide.io/docs/editor/setup/#linux).

Ok, Nuclide zainstalowany i od razu pockerface - otworzyła mi się jakaś zakładka Home z róznymi obcymi dla Atom opcjami. Tutaj z kolei widzisz emotkę z dużymi oczami i otwartą jamą ustną.

![](/images/nuclide-home.jpg)

I to wszystko po to, aby się dowiedzieć, że: _Debugging React Native for Android is currently not supported except for the Simulator logs._ Całe szczęscie okazało się, że to nieprawda i wszystko da się ładnie skonfigurować.    
Przeczytasz o tym w kolejnym artykule, więc stay tuned.


### Zalety
- Opensource
- Bardzo duża ilość pluginów
- Polecany przez Facebook
- Debugger wspierający React Native

### Wady
- Subiektywne wrażenie, że stabilność szwankuje, potrafi się zawieszać,
- Musiałem zainstalować naprawdę sporo pluginów (ok 20) aby był dla mnie używalny,
- Słabo działający (w ogóle?) [Emmet](https://emmet.io/).



## Webstorm
Tutaj nie będę się rozpisywał. Webstorm nie oferuje jakiegoś specjalnego wsparcia dla React Native, ale jestem bardzo zadowolony pracując z "czystym" React. Tak jak już wspomniałem we wstępie, uwielbiam "ux" edytorów ze stajni Jet Brains, a skoro debugować można w przeglądarce, tak samo jak każdą inną aplikację pisaną w javacript, to brak takiej funkcji w IDE nie boli.







## Mój wybór
Mam zamiar poużywać __Nuclide__ z czystej ciekawości. Być może na nowo przekonam się do samego Atoma. 



## Ej, ale to nie wszytkie opcje!
No nie, ale kierowałem się tutaj czasem (wybrać edytor jak najszybciej), swoim systemem operacyjnym (Kubuntu) oraz docelową platformą mobilną (Android).

Ok, nawet tutaj jest jeszcze do wyboru choćby popularny ostatnio [Code](https://code.visualstudio.com/) - opensource edytor od Microsoft. Opensource i Microsoft w jednym zdaniu, które nie jest sarkazmem, skumaj to.   
Ja osobiście go nie polubiłem (go, tego edytora) z uwagi na gorszą, niż Atom, konfigurowalność i o wiele gorsze UX, niż Atom i Webstorm. 

Widziałem jeszcze jakiś spoko edytor dedykowany React Native, ale dostępny tylko na Japko, więc dla biedaka takiego jak ja odpada.

## Dzięki za przeczytanie
Ten post pisałem "na żywo" wybierając edytor, więc podejrzewam iż jeszcze sporo się zmieni w trakcie kodowania. Jeśli tak się stanie, to podzielę się swoimi doświadczeniami w innym poście. Tymczasem myślę, że znalazłem alternatywę dla Webstorm.

Jeśli z czymś się nie zgadzasz, albo masz doświadczenie z innym edytorem, to podziel się proszę w komentarzu. Chętnie sprawdzę Twoje informacje.